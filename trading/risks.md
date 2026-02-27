# Risk Disclosures

**Trading perpetual contracts involves substantial risk of loss and is not suitable for all investors.** Please read this page carefully before trading.

## General Trading Risks

### Leverage Risk

Friction index perpetuals can be traded with up to 20x leverage. While leverage amplifies gains, it equally amplifies losses. A 5% adverse move at 20x leverage results in a 100% loss of your margin (liquidation).

### Liquidation Risk

Positions that fall below the maintenance margin requirement are automatically liquidated by Hyperliquid's engine. Liquidation may result in the complete loss of your deposited margin for that position.

### Funding Rate Risk

Funding rates are exchanged between longs and shorts every hour. Persistent funding costs can erode position value over time, even if the price moves in your favor.

## Index-Specific Risks

### Oracle Risk

Friction's oracle determines the index price used for funding and liquidation calculations. While the oracle is designed with multiple failover levels, risks include:

- Temporary oracle degradation during extreme market events
- Brief price discrepancies between the oracle and market expectations
- Potential for oracle manipulation (mitigated by multi-source design)

### Index Composition Risk

Index composition changes during daily rebalancing (MEME) or when constituent criteria change. This may cause tracking differences from expected behavior.

### HIP-3 Platform Risk

Friction markets operate on Hyperliquid's HIP-3 infrastructure. Risks include:

- **Deployer stake slashing:** If Friction's oracle consistently misbehaves, the HYPE stake could be slashed
- **Market halting:** Hyperliquid can halt any HIP-3 market for safety reasons
- **Infrastructure dependency:** Hyperliquid network issues affect all markets

## Smart Contract & Technical Risks

- Hyperliquid L1 smart contract risks
- Bridge risks when depositing/withdrawing USDC
- Network congestion during high-volatility events
- Front-end interface risks

## Market Risks

- Crypto markets operate 24/7 — prices can change while you sleep
- Extreme volatility can trigger cascading liquidations
- Regulatory changes may impact crypto market access
- Stablecoin (USDC) de-peg risk affecting settlement

## Risk Mitigation

- Never trade with funds you cannot afford to lose
- Use appropriate leverage for your risk tolerance
- Set stop-loss orders to limit downside
- Monitor the stress index for market conditions
- Diversify your portfolio

*This is not financial advice. By trading Friction index perpetuals, you acknowledge and accept all risks described above.*
