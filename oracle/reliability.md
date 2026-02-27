# Oracle Reliability

The Friction oracle is engineered for maximum uptime. A multi-level failover system ensures the oracle continues publishing accurate prices even when individual data sources experience outages.

## Design Philosophy

The oracle follows a strict "never halt" principle. Rather than stopping during partial failures, it degrades gracefully — publishing at reduced confidence while maintaining price continuity.

## Failover Cascade

The system operates across multiple degradation levels:

| Status | Condition | Behavior |
|--------|-----------|----------|
| Normal | All sources healthy | Full cross-validation, highest confidence |
| Degraded | One source failing | Continue with remaining sources, reduced confidence |
| Emergency | Multiple sources failing | Use available data with additional safeguards |
| Last Resort | All primary sources down | Cached values with tight bounds, minimum confidence floor |

## Price Continuity

During failover transitions, the oracle maintains price continuity:

- **No price jumps:** Transitions between source combinations are smoothed
- **Bounds tightening:** Lower confidence = tighter maximum price change per update
- **Cached fallback:** Recent valid prices are cached for short-term emergency use

## Recovery

When a failed source recovers:

1. Source is monitored for stability (not immediately trusted)
2. Data from the recovered source is cross-validated against currently healthy sources
3. Once validated, the source is gradually re-incorporated
4. Confidence increases back to normal levels

## Monitoring & Alerting

- Real-time health checks on all data sources
- Automated alerts on degradation events
- Full audit trail of all failover decisions
- 24/7 team availability for manual intervention if needed

## SLA Targets

| Metric | Target |
|--------|--------|
| Uptime | 99.9%+ |
| Update frequency | Real-time (every few seconds) |
| Source redundancy | N+2 (can lose 2 sources without halting) |
| Recovery time | < 30 seconds after source recovery |
