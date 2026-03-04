# Data Sources

Friction uses a hybrid CEX + DEX architecture. CEX aggregators provide broad market cap coverage; Hyperliquid spot prices provide real-time movement tracking. No single source can influence the final oracle price.

## TCAP Sources

### CEX Layer (Level Anchor)

| Source | Endpoint | Coverage | Update Speed |
|--------|----------|----------|-------------|
| **CoinGecko** | `/api/v3/global` | 13,000+ coins | ~55s server-side cache |
| **CoinMarketCap** | `/v1/global-metrics/quotes/latest` | 10,000+ coins | ~37s server-side cache |

These provide the total crypto market cap used to calculate the TCAP "level." Both are fetched on every oracle cycle and cross-validated.

### DEX Layer (Movement Tracker)

| Source | Endpoint | Coverage | Update Speed |
|--------|----------|----------|-------------|
| **Hyperliquid spot** | `allMids` API | 25 tracked pairs | Sub-second |

Hyperliquid spot prices for 25 major assets (~85% of total market cap) provide tick-by-tick movement between CEX updates. The oracle calibrates a basket ratio against CEX data and uses it to estimate total market cap from HL prices.

### HL Basket Composition

Top 25 assets by market cap weight. The top 5 represent ~70%:

| Rank | Asset | Approx. Weight |
|------|-------|---------------|
| 1 | BTC | ~38% |
| 2 | ETH | ~14% |
| 3 | XRP | ~5% |
| 4 | BNB | ~4% |
| 5 | SOL | ~4% |
| 6-25 | DOGE, ADA, TRX, AVAX, LINK, TON, DOT, MATIC, SHIB, SUI, UNI, AAVE, ARB, OP, APT, NEAR, FIL, INJ, ATOM, SEI | ~20% combined |

## MEME Sources

MEME uses a broader set of sources because memecoins trade across many venues:

| Source | Role | Coverage |
|--------|------|----------|
| **Hyperliquid spot** | Primary | ~30 HL-listed memes |
| **Jupiter** | Primary | All Solana memes |
| **Uniswap V3** | Primary | Ethereum memes |
| **Binance** | Validation | ~50 large-cap memes |
| **Coinbase** | Validation | ~20 large-cap memes |
| **CoinGecko** | Fallback | All tokens (reference pricing) |

Per-token prices are aggregated using a median filter with 5% outlier removal (wider than TCAP's 2% due to higher meme volatility).

## BTC.D Sources

BTC.D reuses the TCAP data pipeline entirely — the oracle already has BTC market cap and total market cap from CoinGecko and CoinMarketCap. No additional API calls needed.

## Cross-Validation

Every oracle update cross-validates sources:

| Check | TCAP Threshold | MEME Threshold |
|-------|---------------|----------------|
| Outlier detection | 2% from median | 5% from median |
| Source agreement | 3+ sources required | 2+ sources required |
| Confidence threshold | 70% agreement | 70% agreement |
| Deviation warning | 1% from reference | 3% from reference |
| Deviation critical | 2% — halt updates | 5% — halt updates |

## Source Health Monitoring

Each source is tracked with a health state machine:

```
unknown → healthy (first success)
healthy → degraded (1 failure)
degraded → unhealthy (3 consecutive failures)
unhealthy → healthy (2 consecutive successes)
```

Metrics tracked per source: status, last success time, consecutive failures, average latency.

## Cost

| Source | Monthly Cost |
|--------|-------------|
| CoinGecko (Analyst plan) | $129 |
| CoinMarketCap (Startup plan) | $95 |
| Hyperliquid spot API | Free |
| Jupiter API | Free |
| Uniswap V3 (The Graph) | Free* |
| **Total** | **~$224/mo** |

*The Graph requires an API key for production rate limits.
