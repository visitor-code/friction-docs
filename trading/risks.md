# Risk Disclosures

{% hint style="danger" %}
**Trading perpetual contracts involves substantial risk of loss and is not suitable for all investors.** You should only trade with funds you can afford to lose. Read this page carefully before trading.
{% endhint %}

## Leverage Risk

Friction markets offer up to 20x leverage (TCAP, BTC.D) and 10x leverage (MEME). Higher leverage amplifies both gains and losses.

| Leverage | Price Move to Lose 50% | Price Move to Liquidation |
|----------|----------------------|--------------------------|
| 2x | 25% | ~50% |
| 5x | 10% | ~20% |
| 10x | 5% | ~10% |
| 20x | 2.5% | ~5% |

{% hint style="warning" %}
At 20x leverage, a 5% adverse move can liquidate your entire position. Use stop-losses and size positions appropriately.
{% endhint %}

## Liquidation Risk

Positions are liquidated by Hyperliquid's liquidation engine when margin falls below the maintenance requirement. Liquidation:

- Closes your position at the current mark price
- Applies a liquidation penalty
- May result in total loss of deposited margin for that position
- Happens automatically with no grace period

## Index Risk

Friction indices are calculated from multiple data sources and may not perfectly track the underlying market:

- **Tracking error:** The index is an approximation of total market cap, not a perfect measurement. Different data providers (CoinGecko, CoinMarketCap) track different token sets.
- **Rebalancing gaps:** The MEME index rebalances daily. Between rebalances, the composition may drift from the intended weights.
- **Rug pull exposure (MEME):** Despite rug detection (80% liquidity drop triggers removal), there is a window of exposure before detection.

## Oracle Risk

The oracle publishes prices every 3 seconds but carries inherent risks:

- **Data source failure:** If multiple data sources go down simultaneously, the oracle degrades to cached pricing at reduced confidence. See [Oracle Reliability](../oracle/reliability.md).
- **Stale pricing:** During failover, published prices may lag the real market by seconds to minutes.
- **Manipulation:** While the hybrid architecture is designed to resist manipulation, no system is perfectly immune. The oracle uses deviation guards, outlier filters, and cross-validation to mitigate this.

## Platform Risk

- **Hyperliquid risk:** All trading occurs on Hyperliquid. Friction does not custody funds. Hyperliquid downtime, bugs, or exploits affect all Friction markets.
- **Smart contract risk:** Hyperliquid's settlement and custody contracts may contain undiscovered vulnerabilities.
- **HIP-3 risk:** As a HIP-3 deployer, Friction's 500K HYPE stake can be slashed by Hyperliquid governance for oracle misbehavior. A slashing event could disrupt market operations.

## Market Risk

- **Crypto volatility:** Cryptocurrency markets are highly volatile. Index prices can move 10%+ in a single day.
- **Correlation risk:** During market stress, assets that are normally uncorrelated may move together, amplifying index moves.
- **Liquidity risk:** During extreme volatility, orderbook depth may thin, leading to slippage on large orders.
- **Funding rate risk:** Funding rates on Hyperliquid perps are variable and can be significant during periods of high demand imbalance.

## Regulatory Risk

- Cryptocurrency perpetual futures may not be legal in all jurisdictions
- Regulatory changes could affect the availability or operation of Hyperliquid and Friction markets
- Users are responsible for understanding and complying with their local regulations

## No Guarantee of Returns

- Past performance of any index does not guarantee future results
- The Stress Index is informational only and should not be used as sole basis for trading decisions
- Index methodology may be updated, which could affect market behavior
