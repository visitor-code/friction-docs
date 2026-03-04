# Oracle Reliability

The oracle is engineered for maximum uptime. A multi-level failover system ensures continuous price publishing even when individual data sources go down.

{% hint style="success" %}
**The oracle never halts.** Even in worst-case scenarios (all sources down), the oracle continues publishing at a minimum confidence floor. Degraded data is better than no data for orderly market function.
{% endhint %}

## Why Uptime Matters

HIP-3 deployers stake 500,000 HYPE (~$15M) that is locked for 30 days after all perpetuals are halted, plus a 7-day unstake queue during which the stake remains slashable. Downtime risks the stake, disrupts trading, and stops fee revenue.

## Failover Levels

The oracle has five graceful degradation levels. Each level is the best the oracle can do given current source availability:

| Level | Name | When | What Happens |
|-------|------|------|-------------|
| **L0** | Normal | All sources healthy | Full hybrid blend at high confidence |
| **L1** | Degraded | One source down | Missing source simulated to maintain price continuity |
| **L2** | Emergency | Primary sources down | Estimation from real-time spot data at reduced confidence |
| **L3** | Cached | All live sources down | Last known price published with alerts |
| **L4** | Last Resort | Everything down | Emergency price at minimum confidence — never halts |

### Source Simulation (L1)

When one source fails, the oracle simulates the missing source using the last known relationship between sources. This avoids sudden price jumps from dropping a source.

{% hint style="warning" %}
**Why simulate instead of dropping?** If two sources consistently differ by a known amount, suddenly switching to one source would cause a price discontinuity. Simulation maintains the blend and prevents unnecessary liquidations.
{% endhint %}

### Emergency Estimation (L2)

When primary aggregator sources are unavailable, the oracle estimates prices from real-time spot data at reduced confidence with tighter bounds.

### Cached Fallback (L3–L4)

If all live data is unavailable, the oracle publishes the last known price at minimum confidence. Critical alerts fire immediately. This is the never-halt guarantee.

## Recovery

When a failed source recovers, the oracle doesn't snap back instantly. A recovery smoother gradually transitions from the degraded state back to normal, preventing price jumps when sources come back online.

## Price Velocity Guards

Maximum price change per update is clamped to market-appropriate limits — tighter for low-volatility macro indices (TCAP, BTC.D), wider for high-volatility sectors (MEME). If a price change exceeds the limit, it is clamped and the original value is logged for investigation.

## Hyperliquid's Defense-in-Depth

Beyond Friction's own guards, Hyperliquid applies a server-side 1% per-update mark price clamp. Even if the oracle publishes a larger move, Hyperliquid smooths it. This provides two independent layers of protection.

## Monitoring & Alerts

The oracle runs continuous monitoring with multi-tier alerting:

- **Source deviation** — escalating alerts when sources disagree
- **Source outages** — immediate alerts when data sources go down
- **Confidence drops** — pages on-call when system health degrades
- **All incidents** — logged with full context for post-incident review

## Backtest Validation

The oracle's parameters are validated against multiple years of historical data covering thousands of data points, including the March 2020 crash, May 2021 crash, and FTX collapse. The safety margins between observed price movements and system limits are significant.
