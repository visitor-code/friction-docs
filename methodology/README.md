# Methodology

Friction deploys three index perpetual markets on Hyperliquid, each backed by a transparent, rules-based methodology. Every index uses the same universal divisor (10 billion) for consistent mental models across products.

### Perpetual Markets (HIP-3)

| Index | Formula | Example |
|-------|---------|---------|
| [TCAP](tcap-index.md) | Total Market Cap / 10B | $3.5T → $350 |
| [BTC.D](btc-dominance.md) | BTC Market Cap / Total Market Cap × 100 | 56% → $56 |
| [MEME](meme-index.md) | Weighted Meme Ecosystem Cap / 10B | $10B → $1.00 |

### Informational Feed

| Index | What It Tracks | Scale |
|-------|---------------|-------|
| [Stress Index](stress-index.md) | Real-time crypto market stress | 18–100 |

{% hint style="info" %}
The Stress Index is an **informational feed only** — it is not a tradeable perpetual on Hyperliquid. It provides real-time stress context for traders and researchers at [friction.market/index/tcap-stress](https://friction.market/index/tcap-stress).
{% endhint %}
