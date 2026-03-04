# Fees

Friction markets use Hyperliquid's HIP-3 fee structure. Fees are slightly higher than standard Hyperliquid markets because they include the cost of oracle infrastructure and index methodology.

## Trading Fees

| Fee Type | Rate | Basis Points |
|----------|------|-------------|
| **Taker** | 0.09% | 9 bps |
| **Maker** | 0.03% | 3 bps |
| **Blended** | ~0.066% | ~6.6 bps |

Blended rate assumes a typical 60/40 taker/maker mix: (9 × 0.60) + (3 × 0.40) = 6.6 bps.

{% hint style="info" %}
HIP-3 markets charge **2x standard Hyperliquid fees** (standard: 4.5 bps taker / 1.5 bps maker). The premium funds the oracle infrastructure that makes index perpetuals possible.
{% endhint %}

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

Friction may activate Hyperliquid's **growth mode** on select markets during early launch phases. Growth mode reduces fees by up to 90%, making Friction markets temporarily cheaper than standard Hyperliquid perps.

When active, fees drop to approximately:

| Fee Type | Growth Mode Rate |
|----------|-----------------|
| Taker | ~0.9 bps |
| Maker | ~0.3 bps |

Growth mode availability is rate-limited by Hyperliquid and will be announced when active.

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
