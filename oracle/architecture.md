# Oracle Architecture

Friction operates a proprietary oracle service that calculates index prices and publishes them to Hyperliquid via the HIP-3 protocol. The oracle is designed for maximum reliability and manipulation resistance.

## Design Principles

1. **Never halt** — Always publish, even at degraded confidence
2. **Never jump** — Price changes must be smooth and continuous
3. **Never trust a single source** — Cross-validate all inputs
4. **Always log** — Full audit trail for every pricing decision

## Pipeline Overview

```
Data Sources -> Aggregation -> Validation -> Publishing -> Hyperliquid
     |              |            |             |
  Fetch from    Median +     Confidence    setOracle()
  multiple      outlier      scoring &     via HIP-3
  sources       filtering    bounds check  API
```

## Aggregation

The oracle fetches market data from multiple independent institutional-grade sources simultaneously. Each source is independently validated and scored:

- **Median filtering:** Takes the median of all available prices, inherently resistant to single-source manipulation
- **Outlier detection:** Sources deviating significantly from the median are flagged and potentially excluded
- **Cross-validation:** Independent source agreement is measured — high agreement increases confidence

## Confidence Scoring

Every oracle update carries a confidence score based on:

- Number of available sources (more is better)
- Agreement between sources (tighter spread = higher confidence)
- Data freshness (stale data reduces confidence)
- Historical consistency (sudden deviations reduce confidence)

## Publishing

Oracle prices are published to Hyperliquid in real time via the HIP-3 deployer API. Hyperliquid uses these prices for:

- Mark price calculation
- Funding rate computation
- Liquidation thresholds

## Monitoring

The oracle runs with comprehensive monitoring and alerting:

- Health checks every few seconds
- Automatic alerts on source failures
- Deviation monitoring between sources
- Full audit logs for regulatory compliance
