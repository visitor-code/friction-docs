# Oracle Architecture

Friction's oracle fetches prices from multiple independent sources, validates and aggregates them, and publishes to Hyperliquid in real time via the HIP-3 `setOracle` API.

## Design Principles

| Principle | What It Means |
|-----------|--------------|
| **Continuous publishing** | Redundant sources and failover ensure uninterrupted price delivery |
| **Smooth pricing** | Graceful transitions between sources — no sudden jumps or discontinuities |
| **Zero trust** | Every input is validated, every output is bounded, sources are cross-checked |
| **Full auditability** | Every pricing decision is logged with complete context |
| **Simulation-first** | All changes are validated against extended historical simulations before production |

## Pipeline

```
Data Sources → Aggregation → Validation → Confidence Scoring → HIP-3 Publishing
```

### 1. Data Fetching

Multiple independent data sources are fetched in parallel on every oracle cycle. Each source returns a market cap or price with a timestamp.

### 2. Hybrid Blending

TCAP uses a hybrid CEX + DEX architecture:

- **CEX layer:** Institutional-grade market data aggregators covering 10,000+ assets provide the "level" — total market cap with broad coverage
- **DEX layer:** Real-time spot prices from deeply liquid markets provide the "movement" — tick-by-tick price tracking between CEX updates

Source weights adjust dynamically based on data freshness. When CEX data is fresh, it anchors the price. As it ages, real-time DEX data takes over. A minimum CEX anchor is always maintained to prevent drift.

### 3. Deviation Guards

If the DEX estimate diverges significantly from CEX data, the oracle forces higher CEX weight to prevent manipulation. Large deviations between any sources trigger protective overrides and elevated monitoring.

### 4. Confidence Scoring

Every oracle update carries a confidence score that reflects source agreement, data freshness, and system health. A minimum confidence floor ensures the oracle always publishes — degraded data is better than no data for orderly market function.

### 5. HIP-3 Publishing

The oracle calls Hyperliquid's `setOracle` with:

| Field | Purpose |
|-------|---------|
| `oraclePxs` | Blended price — used for funding rate and settlement |
| `markPxs` | Anchors mark price (HIP-3 clamps at 1% per update) |
| `externalPerpPxs` | Slow-moving deviation guard |

All markets are batched into a single `setOracle` call.

## Sanity Checks

Multiple layers of sanity checks reject obviously invalid data:

- Prices outside reasonable market cap ranges are rejected
- Per-update price changes are clamped to market-appropriate limits
- Extreme deviations from previous values trigger manual review
- Hyperliquid enforces a 10x maximum daily price range server-side

## Manipulation Resistance

The hybrid architecture makes manipulation extremely difficult:

- **Multi-source validation** — no single source can influence the final price
- **Deviation guards** — force conservative pricing when sources disagree
- **Deeply liquid markets** — the DEX basket tracks major, high-liquidity assets that require enormous capital to move
- **Defense-in-depth** — Hyperliquid's own server-side mark price clamp provides an additional layer of protection beyond the oracle's own guards

{% hint style="info" %}
Manipulating a single mid-cap asset in the DEX basket has negligible impact on the final oracle price due to market-cap weighting. An attacker would need to simultaneously move multiple deeply liquid assets — an economically impractical attack.
{% endhint %}

## Verify the Oracle Yourself

### TCAP

1. Fetch total crypto market cap from [CoinGecko](https://api.coingecko.com/api/v3/global) — look for `total_market_cap.usd`
2. Divide by 10,000,000,000
3. Compare to the published TCAP oracle price

### BTC.D

1. From the same CoinGecko endpoint, get `market_cap_percentage.btc`
2. That percentage is the BTC.D price (e.g., 56.5% = $56.50)

{% hint style="info" %}
Expect ~1–3% deviation between your calculation and the published oracle price due to source timing differences and the hybrid blend. Deviations beyond 3% are investigated automatically.
{% endhint %}
