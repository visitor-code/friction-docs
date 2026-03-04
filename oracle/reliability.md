# Oracle Reliability

The oracle is engineered for maximum uptime. A five-level failover system ensures continuous price publishing even when individual data sources go down.

{% hint style="success" %}
**The oracle never halts.** Even in worst-case scenarios (all sources down), the oracle continues publishing at a minimum 40% confidence floor. Stale data is better than no data for orderly market function.
{% endhint %}

## Why Uptime Matters

HIP-3 deployers stake 500,000 HYPE (~$15M) that is locked for 30 days after all perpetuals are halted, plus a 7-day unstake queue during which the stake remains slashable. Every second of downtime risks the stake and stops fee revenue.

## Failover Levels

| Level | Name | Condition | Confidence | Method |
|-------|------|-----------|-----------|--------|
| **L0** | Normal | Both CG + CMC healthy | 0.95 | Hybrid blend (CEX + HL) |
| **L1** | Degraded | One CEX source down | 0.90 → 0.40 | Simulated source + hybrid blend |
| **L2** | Emergency | Both CEX sources down | 0.55 | HL organic estimation |
| **L3** | Cached | All live sources down | 0.40 | Last known value (2-min TTL) |
| **L4** | Last Resort | All sources + cache expired | 0.40 | Emergency cached price |

### L0 — Normal Operation

Both CoinGecko and CoinMarketCap are returning fresh data. The oracle blends CEX and Hyperliquid prices using staleness-weighted averaging. Basket ratio is recalibrated on every update.

### L1 — Source Simulation

When one CEX source fails, the oracle **simulates** the missing source using the last known deviation between CG and CMC. This avoids a sudden price jump from dropping a source.

- Simulated prices use a frozen deviation ratio from the moment of failure
- Confidence decays over time: 0.90 at start → 0.40 floor after 30+ minutes
- Simulated data is never written to real caches (separate storage)

{% hint style="warning" %}
**Why simulate instead of dropping?** If CoinGecko consistently reads 2% higher than CoinMarketCap, suddenly switching to CMC-only would cause a 1% price drop. Simulation maintains the blend ratio and prevents unnecessary liquidations.
{% endhint %}

### L2 — HL Organic Estimation

Both CEX sources are down. The oracle estimates total market cap purely from Hyperliquid spot prices using the last calibrated basket ratio:

```
TCAP_estimate = (HL_basket_mcap / basket_ratio) / 10B
```

Confidence is reduced to 0.55 with ±2% bounds.

### L3 — Cached Fallback

All live sources are unavailable. The oracle publishes the last known price with a 2-minute TTL cache. Confidence drops to the 0.40 floor. Critical alerts are sent immediately.

### L4 — Last Resort

Cache has expired and no live data is available. The oracle continues publishing the last known price at the 0.40 confidence floor. This is a **never-halt** guarantee — the oracle always publishes.

## Recovery

When a failed source recovers, the oracle doesn't snap back instantly. A recovery smoother uses exponential moving averages to gradually transition from the degraded state back to normal:

- EMA alpha: 0.15 (gradual transition)
- Step cap: ±0.3% per update
- Transition duration: ~2 minutes

This prevents price jumps when sources come back online.

## Price Velocity Guards

Maximum price change per update:

| Market | Max Change | Rationale |
|--------|-----------|-----------|
| TCAP | 0.5% | Low-volatility macro index |
| MEME | 2.0% | High-volatility meme sector |

If a price change exceeds the limit, it is clamped to the maximum and the original value is logged.

## Hyperliquid's Defense-in-Depth

Beyond Friction's own guards, Hyperliquid applies a server-side 1% per-update mark price clamp. Even if the oracle publishes a larger move, Hyperliquid smooths it. This provides two layers of protection.

## Monitoring & Alerts

| Metric | Warning | Critical |
|--------|---------|----------|
| Source deviation (CG vs CMC) | > 3% | > 6% |
| Single source outage | > 1 minute | > 5 minutes |
| Both sources down | Immediate | Immediate |
| Confidence below 70% | Log | Page on-call |
| Simulation age | > 2 minutes | > 5 minutes |

## Backtest Validation

The staleness thresholds are validated against 3 years of hourly TCAP data (26,353 intervals):

| Metric | Value | Safety Margin |
|--------|-------|--------------|
| 95th percentile hourly change | 1.10% | 7x vs HIP-3 1% clamp |
| 80th percentile hourly change | < 0.50% | — |
| 99th percentile hourly change | 2.55% | 3x margin |
| Worst hourly move ever | 19.93% | Distributes across ~1,200 updates at 3s cadence |
