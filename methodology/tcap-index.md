# TCAP Index Methodology

TCAP tracks the total cryptocurrency market capitalization as a single tradeable index. It provides broad market exposure without the complexity of managing individual positions.

## Formula

```
TCAP Price = Total Crypto Market Cap / 10,000,000,000
```

The divisor of 10 billion creates a practical trading price. When the total crypto market cap is $3.5 trillion, TCAP = $350.00.

| Total Market Cap | TCAP Price |
|------------------|------------|
| $2.0 trillion | $200.00 |
| $2.5 trillion | $250.00 |
| $3.0 trillion | $300.00 |
| $3.5 trillion | $350.00 |
| $4.0 trillion | $400.00 |

## What TCAP Includes

TCAP is designed to capture the **entire** crypto market:

- **L1 Blockchains** — BTC, ETH, SOL, ADA, AVAX, etc.
- **L2 & Scaling Solutions** — ARB, OP, MATIC, etc.
- **DeFi Protocols** — UNI, AAVE, MKR, etc.
- **Memecoins** — DOGE, SHIB, PEPE, etc.
- **Exchange Tokens** — BNB, CRO, etc.
- **Stablecoins** — Included as they represent capital deployed in the crypto ecosystem

## Exclusions (Double-Count Prevention)

Tokens that represent claims on an already-counted underlying asset are excluded to prevent double-counting:

- **Wrapped Tokens** — WBTC, WETH, WBNB (1:1 backed by underlying)
- **Liquid Staking Tokens** — stETH, rETH, cbETH, wstETH, mSOL (backed by staked assets)

## Data Methodology

TCAP prices are calculated using data from multiple institutional-grade sources:

- Aggregation across **13,000+ cryptocurrencies**
- Multiple independent data providers for cross-validation
- Manipulation-resistant median filtering
- Real-time updates published to Hyperliquid every few seconds
- Outlier detection and rejection

## Oracle Price Publishing

Oracle prices are published to Hyperliquid via the HIP-3 protocol in real time. Hyperliquid uses these oracle prices for mark price calculation, funding rate computation, and liquidation thresholds.

For more on the oracle infrastructure, see the [Oracle Architecture](../oracle/architecture.md) documentation.

## Historical Context

The total crypto market cap has ranged from under $200 billion (2018 bear market) to over $3.5 trillion (2024 bull market). TCAP allows traders to express a view on the overall direction of the crypto market without picking individual winners.
