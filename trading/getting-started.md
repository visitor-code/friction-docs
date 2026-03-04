# Getting Started

Friction index perpetuals trade directly on Hyperliquid. No separate sign-up required.

## Prerequisites

- A Hyperliquid account ([app.hyperliquid.xyz](https://app.hyperliquid.xyz))
- USDC balance on Hyperliquid (deposit via Arbitrum bridge or direct transfer)
- Any wallet supported by Hyperliquid (MetaMask, Rabby, WalletConnect, etc.)

## Step 1: Connect to Hyperliquid

Go to [app.hyperliquid.xyz](https://app.hyperliquid.xyz) and connect your wallet. If you don't have an account, the first connection creates one.

## Step 2: Fund Your Account

Deposit USDC to your Hyperliquid account. The most common method is bridging USDC from Arbitrum. Hyperliquid also supports direct deposits from other chains.

## Step 3: Find a Friction Market

Search for the market you want to trade:

| Ticker | What It Is |
|--------|-----------|
| **TCAP-USDC** | Total crypto market cap index |
| **BTC.D-USDC** | Bitcoin dominance index |
| **MEME-USDC** | Top memecoins index |

## Step 4: Place a Trade

Friction markets work like any other Hyperliquid perpetual:

1. **Select your side** — Long (market goes up) or Short (market goes down)
2. **Set your size** — How much USDC notional exposure
3. **Choose leverage** — Up to 20x for TCAP and BTC.D, up to 10x for MEME
4. **Pick your order type:**
   - **Market** — Execute immediately at current price
   - **Limit** — Execute at your specified price or better
   - **Stop-Loss** — Close position if price moves against you
   - **Take-Profit** — Close position at your target price
   - **Trailing Stop** — Dynamic stop that follows the price

## Step 5: Manage Your Position

Once filled, your position appears in the Hyperliquid positions panel. You can:

- Adjust leverage
- Add or reduce size
- Set stop-loss and take-profit
- Close partially or fully

## Trading Examples

### Going Long on TCAP

You believe the total crypto market cap will increase from $3.5T to $4T.

- **TCAP price now:** $350 (= $3.5T / 10B)
- **TCAP price target:** $400 (= $4T / 10B)
- **Action:** Long TCAP-USDC at $350
- **If right:** +14.3% gain (× leverage)

### Shorting BTC.D

You believe altcoin season is coming and Bitcoin dominance will drop from 56% to 50%.

- **BTC.D price now:** $56
- **BTC.D target:** $50
- **Action:** Short BTC.D-USDC at $56
- **If right:** +10.7% gain (× leverage)

### Long MEME

You believe the memecoin sector will grow from $10B to $20B total market cap.

- **MEME price now:** $1.00 (= $10B / 10B)
- **MEME target:** $2.00 (= $20B / 10B)
- **Action:** Long MEME-USDC at $1.00
- **If right:** +100% gain (× leverage)

{% hint style="warning" %}
These are illustrative examples only. Past performance does not indicate future results. Trading perpetual futures involves substantial risk of loss. See [Risk Disclosures](risks.md).
{% endhint %}
