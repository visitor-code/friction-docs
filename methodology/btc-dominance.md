# BTC.D Index

BTC.D tracks Bitcoin's share of total cryptocurrency market cap, expressed as a percentage.

## Formula

```
BTC.D = (BTC Market Cap / Total Crypto Market Cap) × 100
```

The price of BTC.D-USDC is the dominance percentage itself. If Bitcoin dominance is 56.5%, the perpetual trades at $56.50.

| BTC Dominance | BTC.D Price |
|--------------|-------------|
| 40% | $40.00 |
| 50% | $50.00 |
| 56.5% (current) | $56.50 |
| 60% | $60.00 |
| 70% | $70.00 |

## Why BTC.D?

Bitcoin dominance is one of the most-watched metrics in crypto. It captures a fundamental market dynamic:

| BTC.D Direction | What It Signals | Market Regime |
|----------------|-----------------|---------------|
| **Rising** (40 → 60) | Capital flowing into BTC, out of alts | Risk-off, "flight to quality" |
| **Falling** (60 → 40) | Capital rotating into altcoins | Risk-on, "altcoin season" |

## Trading Use Cases

- **Altcoin holders:** Long BTC.D to hedge against rotation back to Bitcoin
- **BTC maximalists:** Long BTC.D as a conviction trade
- **Market neutral:** Pair BTC.D with TCAP to isolate rotation vs growth
- **Macro traders:** Express a view on crypto market structure without picking individual tokens

## Data Sources

BTC.D reuses the same infrastructure as TCAP — no additional data sources required. The oracle already has BTC market cap and total market cap from its existing data pipeline, so BTC.D is computed as a simple ratio with zero extra API calls.

See [Oracle Data Sources](../oracle/data-sources.md) for details.

## Market Specifications

| Parameter | Value |
|-----------|-------|
| Ticker | BTC.D-USDC |
| Leverage | Up to 20x |
| Fees | 9 bps taker / 3 bps maker |
| Funding | Standard Hyperliquid (1-hour) |
| Oracle update | Every 3 seconds |
| Collateral | USDC |
