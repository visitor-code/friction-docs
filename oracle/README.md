# Oracle

Friction operates a hybrid CEX+DEX oracle that calculates index prices and publishes them to Hyperliquid via the HIP-3 protocol every 3 seconds.

{% hint style="success" %}
**Core principle:** The oracle never halts. It degrades gracefully through five failover levels, always publishing at the best available confidence.
{% endhint %}

| Page | What You'll Learn |
|------|-------------------|
| [Architecture](architecture.md) | Pipeline design, confidence scoring, and deviation guards |
| [Data Sources](data-sources.md) | CEX + DEX hybrid sourcing with cross-validation |
| [Reliability](reliability.md) | Five-level failover cascade and recovery mechanisms |
