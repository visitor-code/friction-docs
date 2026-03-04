# TCAP Index

TCAP tracks the total cryptocurrency market capitalization as a single tradeable price.

## Formula

```
TCAP Price = Total Crypto Market Cap / 10,000,000,000
```

The 10 billion divisor converts trillions into a tradeable range, similar to how the S&P 500 uses a divisor to produce its index value.

| Total Market Cap | TCAP Price |
|-----------------|------------|
| $2.0 trillion | $200 |
| $2.5 trillion | $250 |
| $3.0 trillion | $300 |
| $3.5 trillion | $350 |
| $5.0 trillion | $500 |
| $10.0 trillion | $1,000 |

## What's Included

TCAP captures **the entire crypto market** — 13,000+ assets tracked by CoinGecko and 10,000+ by CoinMarketCap:

- **Layer 1 blockchains:** BTC, ETH, SOL, AVAX, etc.
- **Layer 2 / scaling:** ARB, OP, MATIC, etc.
- **DeFi:** UNI, AAVE, MKR, etc.
- **Meme coins:** DOGE, SHIB, PEPE, etc.
- **Exchange tokens:** BNB, CRO, etc.
- **Stablecoins:** USDT, USDC, DAI, etc.
- **All other sectors:** AI, gaming, NFT, etc.

{% hint style="warning" %}
**Stablecoins are included** because they represent real capital deployed in the crypto ecosystem. Excluding them would undercount the market.
{% endhint %}

## What's Excluded

Only tokens that would cause double-counting:

| Category | Examples | Reason |
|----------|----------|--------|
| Wrapped tokens | WBTC, WETH, WBNB | 1:1 backed by underlying — already counted |
| Liquid staking tokens | stETH, rETH, cbETH, mSOL | Backed by staked assets — already counted |

## Data Sources

| Source | Coverage | Role |
|--------|----------|------|
| **CoinGecko** | 13,000+ assets | Primary global market cap |
| **CoinMarketCap** | 10,000+ assets | Cross-validation |

Both provide total market cap via their global endpoints. The oracle takes the median when both are available and falls back to single-source if one goes down.

### Source Agreement

| CG/CMC Deviation | Confidence | Action |
|-----------------|------------|--------|
| < 2% | 95% | Normal operation |
| 2–4% | 85% | Elevated monitoring |
| 4–6% | 70% | Reduced confidence |
| > 6% | 60% | Critical alert triggered |

{% hint style="info" %}
CoinGecko tracks ~10,000 tokens and CoinMarketCap ~13,000. A structural deviation of ~3% between sources is normal and expected.
{% endhint %}

## Oracle Updates

| Parameter | Value |
|-----------|-------|
| Update interval | Every 3 seconds |
| HIP-3 minimum | 2.5 seconds |
| Max price change per update | 0.5% (self-imposed) |
| Staleness warning | 5 minutes |
| Max daily range | 10x (HIP-3 enforced) |

## Comparison to Cryptex TCAP

| | Cryptex TCAP | Friction TCAP |
|--|-------------|---------------|
| **Platform** | Ethereum ERC-20 | Hyperliquid HIP-3 |
| **Type** | Spot token (mint/redeem) | Perpetual futures |
| **Divisor** | 10 billion | 10 billion (same) |
| **Leverage** | None | Up to 20x |
| **Speed** | Ethereum block time | Sub-second (Hyperliquid) |

Both use the same 10B divisor, so prices are directly comparable. The key difference: Friction TCAP is a leveraged perpetual on Hyperliquid's orderbook with deep liquidity.

## Historical Reference

| Date | Market Cap | TCAP Price |
|------|-----------|------------|
| Nov 2021 (ATH) | $3.0T | $300 |
| Nov 2022 (FTX crash) | $0.8T | $80 |
| Jan 2024 | $1.7T | $170 |
| Nov 2024 | $3.2T | $320 |
| Feb 2026 | $3.5T | $350 |

## Market Specifications

| Parameter | Value |
|-----------|-------|
| Ticker | TCAP-USDC |
| Leverage | Up to 20x |
| Fees | 9 bps taker / 3 bps maker |
| Funding | Standard Hyperliquid (1-hour) |
| Collateral | USDC |
