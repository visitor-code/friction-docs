# Stress Index

A real-time crypto market stress measurement combining four dimensions of market health into a single 18–100 scale.

{% hint style="info" %}
The Stress Index is an **informational feed only** — not a tradeable perpetual on Hyperliquid. View it live at [friction.market/index/tcap-stress](https://friction.market/index/tcap-stress).
{% endhint %}

## How It Works

The index combines four market stress components, each weighted by its predictive value:

```
Raw Index = 18 + 82 × (0.25 × Fragility + 0.38 × Pressure + 0.30 × Structure + 0.07 × Funding)
```

| Component | Weight | Type | What It Measures |
|-----------|--------|------|-----------------|
| **Fragility** | 25% | Leading | Leverage buildup, funding persistence, imbalance, velocity |
| **Pressure** | 38% | Coincident | Forced selling, volume spikes, cascade acceleration |
| **Structure** | 30% | Coincident | Range expansion, volume anomalies, decay rate |
| **Funding** | 7% | Lagging | Annualized funding rates across major assets |

## Stress Levels

| Level | Range | Frequency | Meaning |
|-------|-------|-----------|---------|
| **Normal** | 18–26 | ~80% of time | Calm markets, base state |
| **Elevated** | 26–34 | ~18% of time | Building tension, early warnings |
| **High** | 34–42 | ~1% of time | Active stress event, elevated risk |
| **Extreme** | 42–100 | ~0.1% of time | Crisis conditions |

The floor is 18 — the index never drops below this in calm markets.

## Settlement Line

The raw index is smoothed using a three-tier adaptive EMA system. The settlement line responds faster as stress increases:

| Tier | When | EMA Weight | Raw Weight | Lookback |
|------|------|-----------|-----------|----------|
| **Normal** | Raw < 26 | 95% | 5% | 12 hours |
| **Elevated** | 26 ≤ Raw < 34 | 85% | 15% | 8 hours |
| **High / Extreme** | Raw ≥ 34 | 80% | 20% | 4 hours |

In normal markets, the settlement line moves slowly (heavy smoothing). During stress events, it responds faster to capture real conditions.

## Data Source

The Stress Index is computed from real-time Hyperliquid WebSocket data across the top 10 assets by weight:

| Asset | Weight |
|-------|--------|
| BTC | 55% |
| ETH | 18% |
| SOL | 5% |
| XRP | 4% |
| BNB | 3% |
| DOGE | 3% |
| ADA | 3% |
| AVAX | 3% |
| LINK | 3% |
| SUI | 3% |

## Why Not a Perp?

The original TCAP-S economic model used a custom funding mechanism where both longs and shorts pay carry (at different rates), with stress and imbalance multipliers. HIP-3 uses Hyperliquid's standard funding rate — the custom carry model cannot be replicated.

The Stress Index is preserved as:

- **Research tool:** Proprietary methodology and historical data
- **Trading context:** Sentiment overlay for TCAP and other Friction market traders
- **Lead generation:** Drives traffic to friction.market
- **Future product:** Premium API, alerts, and subscription features planned

## Dashboard

The live dashboard at [friction.market/index/tcap-stress](https://friction.market/index/tcap-stress) shows:

- **Settlement line** (cyan): Smoothed EMA value — the primary reading
- **Raw index** (red dashed): Unsmoothed real-time value (toggle-able)
- **Component breakdown:** Stacked area chart showing fragility, pressure, structure, and funding
- **EMA panel:** 4-hour, 8-hour, and 12-hour EMA values
- **Level zones:** Color-coded background bands for Normal, Elevated, High, Extreme
