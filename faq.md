# FAQ

## General

### What is Friction?

Friction is a HIP-3 market provider on Hyperliquid. We build crypto index perpetuals — TCAP (total market cap), BTC.D (bitcoin dominance), and MEME (top memecoins). Friction calculates the index prices and publishes them to Hyperliquid via an oracle. Hyperliquid handles all trading, settlement, custody, and liquidations.

### Do I need a Friction account?

No. You trade directly on [Hyperliquid](https://app.hyperliquid.xyz) with your existing wallet and USDC balance. No separate sign-up, deposit, or account required.

### What wallet do I need?

Any wallet supported by Hyperliquid: MetaMask, Rabby, WalletConnect, and others.

### What is HIP-3?

HIP-3 (Hyperliquid Improvement Proposal #3) allows third parties to deploy custom perpetual markets on Hyperliquid by providing oracle prices. The deployer (Friction) stakes HYPE tokens and earns 50% of trading fees. Hyperliquid handles all infrastructure.

## Markets

### What markets does Friction offer?

| Market | What It Tracks | Leverage |
|--------|---------------|----------|
| TCAP-USDC | Total crypto market cap / 10B | Up to 20x |
| BTC.D-USDC | Bitcoin dominance % | Up to 20x |
| MEME-USDC | Top 100 memecoins / 10B | Up to 10x |

### How is TCAP calculated?

`TCAP = Total Crypto Market Cap / 10,000,000,000`. At a $3.5 trillion market cap, TCAP = $350. It uses the same divisor as Cryptex TCAP, so prices are directly comparable. See [TCAP Methodology](methodology/tcap-index.md).

### How is BTC.D calculated?

`BTC.D = (BTC Market Cap / Total Market Cap) × 100`. If Bitcoin dominance is 56%, BTC.D trades at $56. See [BTC.D Methodology](methodology/btc-dominance.md).

### How is MEME calculated?

MEME is a market-cap-weighted index of the top 50–100 memecoins, divided by 10 billion. Tokens are capped at 15% weight individually and 50% for the top 5. Rebalanced daily. See [MEME Methodology](methodology/meme-index.md).

### Why is MEME leverage limited to 10x?

Memecoins are more volatile than the broad market. Lower max leverage reduces liquidation risk during large moves.

## Oracle

### Where do prices come from?

Multiple independent sources: CoinGecko, CoinMarketCap, Hyperliquid spot, Jupiter, Uniswap V3, Binance, and Coinbase. The oracle cross-validates and filters outliers before publishing. See [Data Sources](oracle/data-sources.md).

### How often does the oracle update?

Every 3 seconds for TCAP and BTC.D. Every 2.5 seconds for MEME.

### What happens if a data source goes down?

The oracle has a five-level failover system and never halts. If one source fails, it simulates the missing source using historical deviation data. If all sources fail, it falls back to cached pricing at reduced confidence. See [Reliability](oracle/reliability.md).

### Can the oracle be manipulated?

The hybrid CEX+DEX architecture makes manipulation extremely difficult. Deviation guards cap Hyperliquid's influence, outlier detection filters anomalous prices, and Hyperliquid's own 1% per-update clamp provides defense-in-depth. See [Architecture](oracle/architecture.md).

## Fees

### What are the fees?

9 bps (0.09%) for takers, 3 bps (0.03%) for makers. This is 2x standard Hyperliquid fees because HIP-3 markets include oracle infrastructure costs. See [Fees](trading/fees.md).

### Why are fees higher than regular Hyperliquid markets?

All HIP-3 markets — from any deployer — charge 2x the standard Hyperliquid fee rate. This is a Hyperliquid platform rule, not a Friction surcharge. The structure funds oracle infrastructure and index methodology. Friction does not charge any fees beyond the standard HIP-3 rates.

### Do volume tiers and staking discounts apply?

Yes. Your 14-day Hyperliquid volume tiers and HYPE staking discounts apply to Friction markets just like any other Hyperliquid market. At the highest tiers, effective fees can drop to ~4.5 bps taker / ~0.9 bps maker. See [Fees](trading/fees.md) for the full tier table.

### What is growth mode?

Hyperliquid's growth mode reduces fees by up to 90% on eligible markets. However, crypto index products may not be eligible under current Hyperliquid rules. We will announce if growth mode becomes available for Friction markets.

## Stress Index

### What is the Stress Index?

A real-time crypto market stress monitor on a scale of 18 to 100, combining four market health dimensions: fragility, pressure, structure, and funding. View it at [friction.market/index/tcap-stress](https://friction.market/index/tcap-stress).

### Can I trade the Stress Index?

No. The Stress Index is an informational feed only. It uses a custom funding mechanism that cannot be replicated on HIP-3. It provides trading context for TCAP traders and researchers.

### What do the stress levels mean?

| Level | Range | Meaning |
|-------|-------|---------|
| Normal | 18–26 | Calm markets (~80% of the time) |
| Elevated | 26–34 | Building tension (~18%) |
| High | 34–42 | Active stress event (~1%) |
| Extreme | 42–100 | Crisis conditions (~0.1%) |

## Risk

### Can I lose more than my deposit?

On Hyperliquid, liquidation closes your position before your margin is fully depleted. You cannot lose more than the margin allocated to that position, but you can lose all of it.

### Is my money safe?

Friction does not custody any funds. All deposits, positions, and withdrawals are handled by Hyperliquid. Friction only provides oracle prices.

### What happens if Friction's oracle stops?

The oracle is designed to never halt — it degrades gracefully through five failover levels. In the worst case, Hyperliquid's own mark price system takes over using the last published oracle price until service is restored.
