# Fees

Friction does not charge any fees beyond the standard HIP-3 fee structure set by Hyperliquid. All HIP-3 markets — whether from Friction, trade.xyz, or any other deployer — use the same 2x fee multiplier. This structure funds the oracle infrastructure that makes custom perpetual markets possible.

## Trading Fees

| Fee Type | Rate | Basis Points |
|----------|------|-------------|
| **Taker** | 0.09% | 9 bps |
| **Maker** | 0.03% | 3 bps |
| **Blended** | ~0.066% | ~6.6 bps |

Blended rate assumes a typical 60/40 taker/maker mix: (9 × 0.60) + (3 × 0.40) = 6.6 bps.

{% hint style="info" %}
**Why 2x?** All HIP-3 markets charge 2x the standard Hyperliquid fee (standard: 4.5 bps taker / 1.5 bps maker). This is a Hyperliquid platform rule, not a Friction surcharge. 50% of fees go to the oracle provider (Friction), 50% to Hyperliquid validators.
{% endhint %}

## Volume Discounts

Base fees decrease with your 14-day Hyperliquid trading volume (across ALL markets):

| Tier | 14-Day Volume | Taker | Maker |
|------|--------------|-------|-------|
| Bronze | < $1M | 9.0 bps | 3.0 bps |
| Silver | $1M+ | 8.1 bps | 2.7 bps |
| Gold | $5M+ | 7.2 bps | 2.4 bps |
| Platinum | $25M+ | 6.3 bps | 2.1 bps |
| Diamond | $100M+ | 5.4 bps | 1.5 bps |
| VIP | $250M+ | 4.5 bps | 0.9 bps |

HYPE staking provides an additional 5–40% discount on top of volume tiers.

## Fee Distribution

| Recipient | Share |
|-----------|-------|
| Friction (oracle provider) | 50% |
| Hyperliquid validators | 50% |

## Comparison

| Platform | Taker | Maker |
|----------|-------|-------|
| **Friction (HIP-3)** | 9 bps | 3 bps |
| Hyperliquid (standard) | 4.5 bps | 1.5 bps |
| dYdX | 5 bps | 2 bps |
| Binance Futures | 5 bps | 2 bps |

## Growth Mode

Hyperliquid offers a **growth mode** that reduces fees by up to 90% on eligible markets. Growth mode availability depends on Hyperliquid's eligibility criteria and is rate-limited per deployer.

{% hint style="warning" %}
Crypto index products (including TCAP, BTC.D, and MEME) may not be eligible for growth mode under Hyperliquid's current rules. We will update this page if growth mode becomes available for Friction markets.
{% endhint %}

## No Hidden Fees

| Item | Fee |
|------|-----|
| Deposits | None (Hyperliquid handles) |
| Withdrawals | None (Hyperliquid handles) |
| Account maintenance | None |
| Oracle | Included in trading fee |
| Funding rates | Standard Hyperliquid mechanism (variable, 1-hour intervals) |

## Fee Examples

| Trade | Size | Side | Fee |
|-------|------|------|-----|
| Market buy TCAP | $10,000 | Taker | $9.00 (9 bps) |
| Limit buy TCAP | $10,000 | Maker | $3.00 (3 bps) |
| Market sell MEME | $5,000 | Taker | $4.50 (9 bps) |
| Limit sell BTC.D | $50,000 | Maker | $15.00 (3 bps) |
