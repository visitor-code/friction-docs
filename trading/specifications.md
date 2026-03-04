# Market Specifications

Consolidated parameters for all Friction index perpetuals on Hyperliquid.

## Contract Parameters

| Parameter | TCAP-USDC | BTC.D-USDC | MEME-USDC |
|-----------|-----------|------------|-----------|
| **Underlying** | Total crypto market cap | Bitcoin dominance % | Top 100 memecoins |
| **Formula** | Market Cap / 10B | BTC Cap / Total Cap × 100 | Weighted Ecosystem Cap / 10B |
| **Collateral** | USDC | USDC | USDC |
| **Margin type** | Isolated | Isolated | Isolated |
| **Max leverage** | 20x | 20x | 10x |
| **Taker fee** | 9 bps (0.09%) | 9 bps (0.09%) | 9 bps (0.09%) |
| **Maker fee** | 3 bps (0.03%) | 3 bps (0.03%) | 3 bps (0.03%) |
| **Funding** | 1-hour (HL standard) | 1-hour (HL standard) | 1-hour (HL standard) |
| **Oracle update** | Every 3 seconds | Every 3 seconds | Every 2.5 seconds |
| **Max change/update** | 1% (self-imposed) | 1% (self-imposed) | 2% (self-imposed) |
| **HL mark clamp** | 1% per update | 1% per update | 1% per update |
| **Max daily range** | 10x | 10x | 10x |
| **Outlier threshold** | 2% from median | 2% from median | 5% from median |
| **Min sources** | 3 | 2 | 2 |
| **Rebalancing** | N/A (all assets) | N/A (fixed formula) | Daily 00:00 UTC |

## Fees

Friction markets use the standard HIP-3 fee structure (9 bps taker / 3 bps maker). Friction does not charge any additional fees beyond those set by Hyperliquid — all HIP-3 markets from any deployer use the same 2x fee multiplier.

Your existing Hyperliquid volume tiers and HYPE staking discounts apply automatically. See [Fees](fees.md) for details.

## Price Protections

Multiple layers of protection ensure price accuracy:

| Protection | Value | Enforced By |
|------------|-------|-------------|
| Mark price clamp | ±1% per oracle update | Hyperliquid |
| Max daily range | 10x | Hyperliquid |
| Oracle self-clamp | ±1% (TCAP/BTC.D), ±2% (MEME) | Friction |
| Multi-source validation | Cross-validated across independent sources | Friction |
| Deviation guards | Protective weight overrides when sources disagree | Friction |

See [Oracle Architecture](../oracle/architecture.md) for details on how prices are sourced and validated.
