# MEME Index Methodology

MEME tracks the top 50-100 memecoins by market capitalization, providing exposure to the memecoin ecosystem through a single tradeable index.

## Formula

```
MEME Price = Meme Ecosystem Market Cap / 10,000,000,000
```

Uses the same 10 billion universal divisor as TCAP. When the tracked memecoin ecosystem market cap is $765 million, MEME = $0.077.

## Inclusion Criteria

Tokens must meet all of the following criteria to be included:

| Criterion | Entry Threshold | Exit Threshold |
|-----------|-----------------|----------------|
| Classification | Must be classified as a memecoin by major data providers | — |
| Market Cap | $10M+ | $8M (80% hysteresis) |
| Liquidity | $500K+ on-chain | $400K |
| Token Age | 7+ days since creation | — |
| DEX Availability | Available on major decentralized exchanges | — |

Hysteresis thresholds (exit lower than entry) prevent tokens from rapidly entering and exiting the index near the boundary.

## Exclusions

- Stablecoins
- Wrapped tokens
- Tokens flagged as rugged or fraudulent

## Weighting

MEME uses a hybrid market cap + liquidity weighting methodology:

- Base weight derived from market capitalization
- Liquidity adjustment factor (0.5x to 1.5x) rewards tokens with deep on-chain liquidity
- Volume quality score contributes to the combined weight

### Weight Caps

| Cap Type | Limit |
|----------|-------|
| Single Token Maximum | 15% |
| Top 5 Combined Maximum | 50% |
| Minimum Weight | 0.1% |

## Rebalancing

The index is rebalanced **daily at 00:00 UTC**:

1. Fetch all tokens meeting the memecoin classification
2. Apply inclusion criteria filters
3. Calculate new weights with caps applied
4. Compare to previous composition — log additions, removals, and weight changes
5. Update oracle service with new composition

## Emergency Removal

Tokens may be removed outside the daily rebalance window under emergency conditions:

- **Rug detection:** If liquidity drops more than 80% within one hour, the token is immediately removed
- Removed weight is redistributed proportionally among remaining constituents
- Emergency removals are logged and reported

## Data Sources

MEME prices are sourced primarily from decentralized exchanges where memecoins trade:

- Multiple Solana DEX aggregators for price discovery
- On-chain liquidity depth verification
- Cross-validation against centralized exchange listings where available
- Manipulation-resistant median filtering across sources
