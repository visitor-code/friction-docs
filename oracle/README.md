# Oracle Infrastructure

How prices are sourced, validated, and published to Hyperliquid.

{% hint style="success" %}
**Core principle:** The oracle never halts. It degrades gracefully through multiple failover levels, always publishing at the best available confidence.
{% endhint %}

| Page | What You'll Learn |
|------|-------------------|
| [Architecture](architecture.md) | Hybrid pipeline design, validation, and deviation guards |
| [Data Sources](data-sources.md) | Multi-source CEX + DEX architecture with cross-validation |
| [Reliability](reliability.md) | Multi-level failover and recovery mechanisms |
