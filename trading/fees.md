# Fee Structure

Friction index perpetuals use Hyperliquid's HIP-3 fee structure. Fees are slightly higher than standard Hyperliquid markets (2x multiplier) to compensate for the custom oracle infrastructure.

## Trading Fees

| Fee Type | Rate | Notes |
|----------|------|-------|
| Taker Fee | 9 bps (0.09%) | Standard Hyperliquid taker x 2x HIP-3 multiplier |
| Maker Fee | 3 bps (0.03%) | Standard Hyperliquid maker x 2x HIP-3 multiplier |
| Funding Rate | Variable | Standard Hyperliquid 1-hour funding |

### Blended Fee Rate

Assuming a typical 60/40 taker/maker mix:

```
Blended = (9 x 0.60) + (3 x 0.40) = 6.6 bps per trade
```

## Fee Distribution

| Recipient | Share |
|-----------|-------|
| Friction (oracle provider) | 50% |
| Hyperliquid validators | 50% |

## Fee Comparison

| Platform | Taker | Maker |
|----------|-------|-------|
| Friction (HIP-3) | 9 bps | 3 bps |
| Hyperliquid (standard) | 4.5 bps | 1.5 bps |
| dYdX | 5 bps | 2 bps |
| Binance Futures | 5 bps | 2 bps |
| CME Bitcoin Futures | ~5-6 bps | ~2-3 bps |

While HIP-3 fees are higher than standard Hyperliquid markets, they are competitive with other exchanges. The premium reflects the cost of maintaining institutional-grade index methodology and real-time oracle infrastructure.

## Growth Mode

Hyperliquid's HIP-3 protocol supports a "growth mode" that can reduce fees by up to 90% for selected markets. Friction may activate growth mode during the early launch phase to drive volume and attract traders.

## No Hidden Fees

- No deposit or withdrawal fees (handled by Hyperliquid)
- No account maintenance fees
- No additional oracle fees
- Funding rates are the standard Hyperliquid mechanism
