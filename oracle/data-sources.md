# Data Sources

Friction's oracle infrastructure aggregates data from multiple independent, institutional-grade data providers. This multi-source approach ensures no single provider can influence the oracle price.

## Source Requirements

Each data source must meet the following criteria to be included in the oracle:

- **Independence:** Independently operated infrastructure
- **Coverage:** Comprehensive cryptocurrency market coverage
- **Latency:** Real-time or near real-time data availability
- **Track record:** Proven reliability with institutional users
- **Commercial terms:** Appropriate licensing for commercial oracle use

## Source Categories

### TCAP (Total Market Cap)

TCAP requires aggregation across 13,000+ cryptocurrencies, which necessitates comprehensive market data providers that cover the full spectrum of the crypto market. Multiple independent providers are used and cross-validated against each other.

### MEME (Memecoin Index)

Memecoin pricing is sourced primarily from decentralized exchanges where these tokens trade. On-chain price discovery from multiple DEX protocols ensures accurate valuation even for less liquid tokens.

### BTC.D (Bitcoin Dominance)

BTC.D uses the same underlying data as TCAP — Bitcoin market cap divided by total market cap. Both numerator and denominator use the same cross-validated sources for consistency.

## Manipulation Resistance

- **No single source dependency:** Oracle always requires multiple source agreement
- **Median filtering:** Extreme values from any source are naturally filtered
- **Confidence weighting:** Sources with consistent, fresh data carry more weight
- **Bounds checking:** Maximum price change per update is clamped to prevent flash manipulation
- **Cross-validation:** Sources are compared against each other — significant disagreement triggers alerts

## Source Health Monitoring

Each source is continuously monitored for:

- Response latency
- Data staleness
- Deviation from other sources
- API availability and error rates

Degraded sources are automatically flagged and may be temporarily excluded from the aggregation. See [Reliability](reliability.md) for details on the failover system.
