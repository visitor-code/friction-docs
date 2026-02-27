# Stress Index (TCAP-S)

The Friction Stress Index is a real-time market stress measurement combining four dimensions of crypto market health into a single 18-100 scale. It is published as an informational feed, not as a tradeable perpetual.

**Live monitor:** [friction.market/index/tcap-stress](https://friction.market/index/tcap-stress)

## Components

| Component | Weight | Type | What It Measures |
|-----------|--------|------|------------------|
| Fragility | 30% | Leading | Real-time volatility measurement |
| Liquidation | 20% | Coincident | Open interest changes + volume pressure |
| Structure | 35% | Coincident | Spread widening + price momentum |
| Funding | 15% | Lagging | Funding rate extremes |

## Stress Levels

| Level | Range | Interpretation |
|-------|-------|----------------|
| Normal | 18 - 26 | Markets functioning normally, low volatility |
| Elevated | 26 - 34 | Above-average stress, increased caution warranted |
| High | 34 - 42 | Significant stress, expect elevated volatility |
| Extreme | 42+ | Extreme market stress, crisis conditions |

## Adaptive Smoothing

The index uses three-tier adaptive EMA (Exponential Moving Average) smoothing that becomes more responsive as stress increases:

- **Normal conditions:** Heavier EMA smoothing filters out noise
- **Elevated conditions:** More responsive to changes
- **High/Extreme conditions:** Fastest response for crisis detection

This means the index reacts faster during genuine crises while filtering out noise during calm periods.

## Use Cases

- **Trading context:** Overlay stress data on your TCAP positions
- **Risk management:** Reduce exposure when stress enters High/Extreme zones
- **Research:** Historical stress analysis for market regime identification
- **Alerts:** Set up notifications for stress level changes

## Data Sources

The stress index aggregates data from Hyperliquid's real-time WebSocket feed, including price action, funding rates, open interest, and order book depth across major perpetual markets.
