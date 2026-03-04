# Friction

Crypto index perpetuals on Hyperliquid. Trade the entire market — or any sector — in a single position.

{% hint style="info" %}
Friction is a **HIP-3 market provider** on Hyperliquid. We build index methodology and oracle infrastructure. Hyperliquid handles all trading, settlement, and custody.
{% endhint %}

## Markets

| Market | What You Trade | Leverage | Status |
|--------|---------------|----------|--------|
| **TCAP-USDC** | Total crypto market cap ($3.5T → $350 TCAP) | Up to 20x | Launching |
| **BTC.D-USDC** | Bitcoin dominance (56% → $56 BTC.D) | Up to 20x | Coming soon |
| **MEME-USDC** | Top 100 memecoins by market cap | Up to 10x | Coming soon |

No separate account needed — trade directly on [Hyperliquid](https://app.hyperliquid.xyz) with your existing wallet and USDC balance. All standard order types work: Market, Limit, Stop-Loss, Take-Profit, and Trailing Stop.

## How It Works

1. **Friction calculates index prices** from multiple data sources (CoinGecko, CoinMarketCap, Hyperliquid spot, Jupiter, Uniswap)
2. **Friction publishes prices** to Hyperliquid every 3 seconds via the HIP-3 oracle API
3. **Hyperliquid handles everything else** — matching, positions, liquidations, funding, custody
4. **You trade** index perpetuals like any other Hyperliquid market

## Documentation

### [Index Methodology](methodology/README.md)

How each index is calculated, what's included, and how it's maintained.

| Index | What It Tracks |
|-------|---------------|
| [TCAP](methodology/tcap-index.md) | Total crypto market cap divided by 10 billion. Covers 13,000+ assets. |
| [BTC.D](methodology/btc-dominance.md) | Bitcoin's share of total crypto market cap, expressed as a percentage. |
| [MEME](methodology/meme-index.md) | Top 50–100 memecoins, market-cap weighted with caps, daily rebalanced. |
| [Stress Index](methodology/stress-index.md) | Real-time market stress monitor (informational feed, not a perp). |

### [Oracle Infrastructure](oracle/README.md)

How prices are sourced, validated, and published to Hyperliquid.

| Page | What You'll Learn |
|------|-------------------|
| [Architecture](oracle/architecture.md) | Hybrid CEX+DEX pipeline with confidence scoring and deviation guards. |
| [Data Sources](oracle/data-sources.md) | Five data sources with cross-validation and outlier detection. |
| [Reliability](oracle/reliability.md) | Five-level failover — the oracle never halts. |

### [Trading](trading/README.md)

Everything you need to start trading Friction index perpetuals.

| Page | What You'll Learn |
|------|-------------------|
| [Getting Started](trading/getting-started.md) | Connect your wallet, fund your account, place your first trade. |
| [Market Specifications](trading/specifications.md) | All contract parameters, fee tiers, and price bounds in one table. |
| [Fees](trading/fees.md) | Fee structure, volume discounts, and staking benefits. |
| [Risk Disclosures](trading/risks.md) | Leverage, liquidation, oracle, slashing, and platform risks. |

---

**Questions?** See the [FAQ](faq.md).
