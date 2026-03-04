# Oracle Architecture

Friction's oracle fetches prices from multiple independent sources, validates and aggregates them, and publishes to Hyperliquid every 3 seconds via the HIP-3 `setOracle` API.

## Design Principles

Five rules govern all oracle code:

| # | Rule | Meaning |
|---|------|---------|
| 1 | **Never halt** | Always publish, even at degraded confidence (floor: 40%) |
| 2 | **Never jump** | Price changes must be smooth — simulate failed sources rather than switching abruptly |
| 3 | **Never trust** | Validate all inputs, bound all outputs, cross-validate across sources |
| 4 | **Always log** | Every pricing decision logged with full context for audit |
| 5 | **Always test** | 48-hour simulation minimum before any production deploy |

## Pipeline

```
Data Sources → Aggregation → Confidence Scoring → HIP-3 Publishing
```

### 1. Data Fetching

All sources are fetched in parallel every 3 seconds. Each source returns a market cap or price with a timestamp.

### 2. Hybrid Blending (TCAP)

TCAP uses a hybrid CEX+DEX architecture:

- **CEX layer** (CoinGecko + CoinMarketCap): Provides the "level" — total market cap from 13,000+ assets
- **Hyperliquid layer** (25 spot pairs): Provides the "movement" — tick-by-tick price changes from deeply liquid markets covering ~85% of total market cap

The blend weight shifts based on how fresh the CEX data is:

| CEX Data Age | CEX Weight | HL Weight | Rationale |
|-------------|-----------|-----------|-----------|
| < 15 seconds | 60% | 40% | CEX just refreshed, high confidence |
| 15–30 seconds | 40% | 60% | CEX aging, HL tracks movement better |
| 30–45 seconds | 20% | 80% | CEX stale, HL dominates |
| > 45 seconds | 5% | 95% | CEX very stale, HL near-solo (5% anchor prevents drift) |

### 3. Deviation Guard

If the Hyperliquid estimate diverges from CEX by more than 2%, the oracle forces at least 70% CEX weight to prevent manipulation:

```
if |HL_estimate - CEX_price| / CEX_price > 2%:
    CEX weight = max(current_weight, 70%)
```

### 4. Confidence Scoring

Every oracle update carries a confidence score (0.40 – 0.95):

| Factor | Effect |
|--------|--------|
| Source agreement (CG vs CMC) | Deviation < 2% = 0.95, > 6% = 0.60 |
| Staleness | Fresh (< 30s) = 1.0x, Critical (45-60s) = 0.7x, Halt (> 60s) = 0.0x |
| Failover level | L0 = 0.95, L1 = 0.90 → 0.40, L2 = 0.55, L3/L4 = 0.40 |

```
Final confidence = base × failover_multiplier × staleness_multiplier
```

### 5. HIP-3 Publishing

Every 3 seconds, the oracle calls Hyperliquid's `setOracle` with:

| Field | Value | Purpose |
|-------|-------|---------|
| `oraclePxs` | Blended price | Used for funding rate and settlement |
| `markPxs` | Same as oracle | Anchors mark price (HIP-3 clamps at 1% per update) |
| `externalPerpPxs` | EMA of recent marks | Slow-moving deviation guard |

All markets are batched into a single `setOracle` call.

## Verify the Oracle Yourself

It is important that market participants can independently replicate and verify oracle prices. Here's how:

### TCAP

1. Fetch total crypto market cap from [CoinGecko](https://api.coingecko.com/api/v3/global) — look for `total_market_cap.usd`
2. Divide by 10,000,000,000
3. Compare to the published TCAP oracle price

### BTC.D

1. From the same CoinGecko endpoint, get `market_cap_percentage.btc`
2. That percentage is the BTC.D price (e.g., 56.5% → $56.50)

### MEME

MEME requires fetching individual token prices and applying weights. The full composition and weights are published daily. Contact Friction for the current composition snapshot.

{% hint style="info" %}
Expect ~1-3% deviation between your calculation and the published oracle price due to source timing differences and the hybrid blend. Deviations beyond 3% are investigated automatically.
{% endhint %}

## Sanity Checks

| Check | Threshold | Action |
|-------|-----------|--------|
| Min total market cap | $100 billion | Reject if below |
| Max total market cap | $50 trillion | Reject if above |
| Max daily price range | 10x | HIP-3 enforced |
| Max per-update change | 0.5% (TCAP) / 2% (MEME) | Self-imposed clamp |
| Deviation > 50% from previous | — | Manual review required |

## Manipulation Resistance

The hybrid architecture makes manipulation extremely difficult:

- **BTC + ETH = ~52% of HL basket weight** — moving them requires enormous capital
- **2% deviation guard** forces CEX dominance if HL diverges
- **Even at max HL weight (95%)**, an attacker must move 25 deeply liquid assets simultaneously
- **Hyperliquid's own 1% per-update clamp** provides defense-in-depth beyond the oracle's guards

{% hint style="info" %}
Example: Moving SEI by 50% (0.3% of basket weight) at max HL weight (95%) moves the blend by just 0.14%.
{% endhint %}
