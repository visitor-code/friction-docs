# MEME Index

MEME tracks the top 50–100 memecoins by market cap, giving diversified exposure to the memecoin ecosystem through a single tradeable index.

## Formula

```
MEME Price = Weighted Sum(token_mcap × weight) / 10,000,000,000
```

The same 10 billion divisor used across all Friction indices. Sub-dollar pricing creates a natural "upside potential" feel.

| Meme Ecosystem Cap | MEME Price |
|-------------------|------------|
| $500 million | $0.05 |
| $5 billion | $0.50 |
| $10 billion | $1.00 |
| $50 billion | $5.00 |
| $100 billion | $10.00 |

## Token Selection

### Inclusion Criteria

| Criteria | Threshold |
|----------|-----------|
| Market cap | $10M+ to enter, $8M to exit |
| Liquidity | $500K+ to enter, $400K to exit |
| Age | 7+ days since creation |
| Classification | Listed in major aggregator memecoin categories |

{% hint style="info" %}
**Hysteresis prevents churn.** Entry thresholds are 25% higher than exit thresholds so tokens don't constantly flip in and out of the index.
{% endhint %}

### What's Included

MEME covers memecoins across all chains — not just Solana:

- **Established memes:** DOGE, SHIB, PEPE, WIF, BONK, FLOKI
- **Pump.fun graduates:** Tokens that passed Raydium migration on Solana
- **Cross-chain memes:** Tokens on Ethereum, Base, BNB Chain

### What's Excluded

- Stablecoins and wrapped tokens
- Tokens below exit thresholds
- Rugged tokens (detected by 80%+ liquidity drop in 1 hour)

## Weighting

Weights are based on market cap with caps to prevent concentration:

| Cap | Value | Purpose |
|-----|-------|---------|
| Single token max | 15% | No single coin dominates |
| Top 5 combined max | 50% | Ensures diversification |
| Minimum weight | 0.1% | Excludes dust positions |

### Weight Calculation

1. Calculate raw weight from market cap: `token_mcap / total_ecosystem_mcap`
2. Cap individual tokens at 15%
3. If top 5 exceed 50% combined, scale them down proportionally
4. Remove tokens below 0.1% minimum
5. Normalize all weights to sum to 1

## Rebalancing

### Daily (00:00 UTC)

1. Fetch all qualifying tokens from market data aggregators
2. Apply inclusion criteria (new tokens must meet entry thresholds)
3. Calculate and cap weights
4. Update composition
5. Log all additions, removals, and weight changes

### Emergency (Rug Detection)

If a token's liquidity drops more than 80% within 1 hour:

1. Immediately remove from index
2. Redistribute weight proportionally to remaining tokens
3. Critical alert sent to team
4. Token must re-qualify from scratch to re-enter

## Data Sources

MEME uses a broad set of sources across CEX and DEX venues because memecoins trade on many platforms:

- **DEX aggregators** — Solana, Ethereum, and other chain DEXs (primary pricing)
- **Hyperliquid spot** — HL-listed memecoins
- **Major centralized exchanges** — cross-validation
- **Market data aggregators** — fallback reference pricing

Per-token price aggregation:
- Collect prices from all available sources
- Apply median filter with outlier removal (wider threshold than TCAP due to meme volatility)
- Weighted average of remaining sources

See [Oracle Data Sources](../oracle/data-sources.md) for details on the multi-source architecture.

## Market Specifications

| Parameter | Value |
|-----------|-------|
| Ticker | MEME-USDC |
| Leverage | Up to 10x (higher volatility) |
| Fees | 9 bps taker / 3 bps maker |
| Funding | Standard Hyperliquid (1-hour) |
| Oracle update | Every 2.5 seconds |
| Outlier threshold | 5% (vs 2% for TCAP) |
| Max price change per update | 2% (vs 1% for TCAP) |
| Collateral | USDC |
