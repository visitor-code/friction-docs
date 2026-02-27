# Getting Started

Friction index perpetuals trade directly on Hyperliquid. No additional accounts, wallets, or sign-ups are needed — use your existing Hyperliquid account.

## Prerequisites

1. **Hyperliquid account** — Visit [app.hyperliquid.xyz](https://app.hyperliquid.xyz) and connect your wallet
2. **USDC on Hyperliquid** — Bridge USDC from Arbitrum to Hyperliquid L1
3. That's it.

## Step-by-Step

### 1. Find Friction Markets

On Hyperliquid's trading interface, search for:

- **TCAP-USDC** — Total crypto market cap index
- **BTC.D-USDC** — Bitcoin dominance index (coming soon)
- **MEME-USDC** — Top 100 memecoin index (coming soon)

### 2. Place Your Trade

Friction markets work exactly like any other Hyperliquid perpetual:

- Choose **Long** (bullish) or **Short** (bearish)
- Set your position size in USDC
- Select leverage (up to 20x for TCAP and BTC.D, up to 10x for MEME)
- Use Market or Limit order type
- Confirm the trade

### 3. Manage Your Position

All position management features are native Hyperliquid:

- Real-time P&L tracking
- Stop-loss and take-profit orders
- Adjust leverage on open positions
- Partial close capabilities

## Key Concepts

### How Index Perpetuals Differ

Unlike single-asset perpetuals (BTC-USDC, ETH-USDC), Friction's index perpetuals track a basket of assets. This means:

- **Diversified exposure:** One position covers the entire market or sector
- **Lower single-asset risk:** No exposure to individual token events
- **Oracle-priced:** Friction's oracle determines the index price, not the order book

### Funding Rates

Friction markets use Hyperliquid's standard 1-hour funding rate mechanism. Funding is exchanged between longs and shorts based on the difference between the mark price and the oracle price.

### Liquidation

Liquidation works the same as any Hyperliquid perpetual — if your margin falls below the maintenance requirement, your position is liquidated by Hyperliquid's engine.
