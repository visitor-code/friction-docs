# Data Sources

Friction uses a hybrid CEX + DEX architecture. Institutional-grade aggregators provide broad market cap coverage; real-time spot prices from decentralized and centralized exchanges provide movement tracking. No single source can influence the final oracle price.

## TCAP Sources

### CEX Layer (Level Anchor)

Multiple institutional-grade market data aggregators provide total crypto market cap covering 10,000–13,000+ assets. These form the "level" anchor for the TCAP price.

Both primary sources are fetched on every oracle cycle and cross-validated against each other. If they diverge beyond acceptable thresholds, monitoring alerts are triggered.

### DEX Layer (Movement Tracker)

Real-time spot prices from a diversified basket of major assets covering the majority of total crypto market cap. These provide tick-by-tick movement between CEX refreshes.

The oracle calibrates a basket ratio against CEX data and uses it to estimate total market cap from spot prices in real time.

## MEME Sources

MEME uses a broader set of sources because memecoins trade across many venues:

- **Hyperliquid spot** — listed memecoins
- **Solana DEX aggregators** — all Solana memecoins
- **Ethereum DEX** — Ethereum memecoins
- **Major CEXs** — large-cap memecoins (validation)
- **Market data aggregators** — reference pricing (fallback)

Per-token prices are aggregated using a median filter with outlier removal. MEME uses a wider outlier threshold than TCAP due to higher memecoin volatility.

## BTC.D Sources

BTC.D reuses the TCAP data pipeline entirely — the oracle already has BTC market cap and total market cap from its CEX sources. No additional API calls needed.

## Cross-Validation

Every oracle update cross-validates sources with market-appropriate thresholds:

- **Outlier detection** — prices that deviate significantly from the median are filtered
- **Multi-source agreement** — minimum source count required before publishing
- **Confidence scoring** — deviation between sources reduces confidence proportionally
- **Automated alerting** — escalating alerts when sources disagree beyond expected ranges

## Source Health Monitoring

Each data source is tracked with a health state machine that transitions between healthy, degraded, and unhealthy states based on consecutive successes and failures. Metrics tracked per source include status, last success time, failure count, and average latency.

Source health directly influences the oracle's confidence score and failover behavior.
