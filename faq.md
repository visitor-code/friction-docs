# Frequently Asked Questions

## General

### What is Friction?

Friction is a HIP-3 market provider on Hyperliquid that deploys crypto index perpetual contracts. We build the index methodology and oracle infrastructure — Hyperliquid handles all trading execution, settlement, and custody.

### What markets does Friction offer?

Three markets under a single portfolio:

- **TCAP-USDC** — Total crypto market cap index (live)
- **BTC.D-USDC** — Bitcoin dominance index (coming soon)
- **MEME-USDC** — Top 100 memecoin index (coming soon)

### Do I need a separate account?

No. Friction markets trade directly on Hyperliquid. Use your existing Hyperliquid account and USDC balance.

### What is HIP-3?

HIP-3 is Hyperliquid's protocol for third-party perpetual contract deployment. It allows external teams to provide oracle prices while Hyperliquid handles all trading infrastructure. See the [Hyperliquid HIP-3 docs](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals).

## Index Questions

### What is TCAP?

TCAP = Total Crypto Market Cap / 10 Billion. It tracks the entire crypto market in a single price. When crypto is $3.5 trillion, TCAP = $350.

### Why not just trade BTC?

TCAP provides diversified crypto exposure. If you're bullish on crypto broadly but don't want to pick individual winners, TCAP lets you trade the whole market in one position.

### What's included in TCAP?

All cryptocurrencies including L1s, L2s, DeFi, memes, exchange tokens, and stablecoins. Wrapped tokens and liquid staking tokens are excluded to prevent double-counting. See the [full methodology](methodology/tcap-index.md).

### How is MEME different from buying individual memecoins?

MEME tracks 50-100 memecoins with automatic rebalancing. It reduces single-token risk and captures the overall memecoin sector trend without picking winners.

### How often does MEME rebalance?

Daily at 00:00 UTC, plus emergency removals for rug events (80%+ liquidity drop in 1 hour).

## Trading Questions

### What leverage is available?

TCAP and BTC.D: up to 20x. MEME: up to 10x (reduced due to higher volatility). These are the maximum — you can use any leverage up to these limits.

### What are the fees?

Taker: 9 bps (0.09%), Maker: 3 bps (0.03%). Standard Hyperliquid fees with 2x HIP-3 multiplier. See [fee details](trading/fees.md).

### How does funding work?

Standard Hyperliquid 1-hour funding rates. Funding is exchanged between longs and shorts based on the difference between mark price and oracle price.

### Can I use limit orders?

Yes. All Hyperliquid order types work: Market, Limit, Stop-Loss, Take-Profit, and Trailing Stop.

### How are positions liquidated?

Liquidation follows standard Hyperliquid rules. If your margin falls below maintenance requirements, Hyperliquid's engine liquidates your position.

## Oracle Questions

### Where does the price data come from?

Multiple independent, institutional-grade data sources. The oracle uses median filtering and cross-validation to prevent any single source from influencing the price. See [data sources](oracle/data-sources.md).

### How often is the oracle updated?

Real-time — new prices are published to Hyperliquid every few seconds.

### What happens if the oracle fails?

The oracle has a five-level failover system. It never halts — it degrades gracefully, publishing at reduced confidence with tighter bounds. See [reliability](oracle/reliability.md).

## Risk Questions

### Can I lose more than my margin?

No. Hyperliquid perpetuals have isolated margin — your maximum loss is the margin allocated to each position. You cannot go into negative balance.

### Is there a risk of the oracle being manipulated?

The oracle uses multiple independent sources with median filtering, making single-source manipulation ineffective. See [oracle architecture](oracle/architecture.md).

### What happens during extreme market events?

The oracle is designed to perform under stress. It uses adaptive smoothing and may tighten price bounds during extreme volatility. Monitor the stress index for real-time conditions.

## Support

### How do I get help?

Visit our support page to submit a ticket, chat with us on Crisp, or join our Discord community.
