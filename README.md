# RWA

Supplementary experiments for real-world asset integration in next-generation communication networks.

| PDF | Experiment |
| --- | --- |
| [Capital liquidity](capital_liquidity.pdf) | Time-dependent net cash returns under limited initial funding. |
| [Granularity](ablation_allocation.pdf) | Finer indivisible lots raise useful utilization under budget-constrained buyers. |
| [Security self-ablation](ablation_robustness.pdf) | RWA with/without AMM pricing or on-chain payment enforcement. |
| [Leasing notes](Supplementary%20Notes%20for%20Leasing%20Mode.pdf), [leasing figure](leasing.pdf) | Existing resource-reuse and cumulative user-satisfaction experiment. |

## Capital liquidity

The firm needs 30% of a resource costing 100 normalized units. It starts with 10 units, accumulates 3 per epoch from existing business, and earns 5 per epoch once the required capacity is available. Leasing costs 3 per epoch; fractional purchase costs 30 and whole-block purchase costs 100. Unused whole-block capacity produces no extra income.

Returns deduct acquisition payments or recurring rent. Background savings determine purchase timing but are excluded from returns; residual asset value and rent-to-buy switching are also excluded. Purchase costs cause the downward jumps. Fractional and whole-block purchases start at epochs 6.67 and 30 and overtake leasing at 21.11 and 83.33.

## RWA self-ablations

The self-ablations isolate individual mechanisms under paired inputs: 100 sellers with 1 to 5 resources each, shared physical supply/demand and buyer cash across conditions, and the same constant-product pricing; only recorded seller inventory can be delivered.

**Granularity.** A resource block costs 30 and is split into 3, 30, or 300 indivisible tokens, so the minimum tradable unit is 1/N of a block and the minimum ticket is 30/N. All seller capacity is escrowed into a constant-product pool; 100 to 300 buyers, each with a fixed budget of 60 to 240, trade whole tokens in a paired random order. The metric is **useful resource utilization**, defined as acquired capacity matched to demand divided by initial physical capacity, rather than whole-block completion, which hides partial sales.

Useful utilization is higher with finer lots at every buyer count (3 < 30 < 300). Finer splits lower the entry barrier because the minimum ticket 30/N falls, so budget-constrained buyers can participate with smaller budgets and purchase closer to their actual demand with less overpurchase of the last indivisible token. 为了突出细粒度的影响，我们的配置和原文略有不同。

**Security.** All panels use 200 buyers, 100 liquidity providers, 30 tokens per resource and 0–30% malicious participants. The common metric is final **paid resource allocation / initial physical capacity**.

- **Seller collusion:** compare full RWA with RWA without AMM. Malicious sellers raise asks by 1.2–1.5 times and reduce their listing rate to 30%; this slows release rather than permanently deleting capacity.
- **Buyer collusion:** compare the same AMM switch. Malicious buyers lower bids to 60–80% and spending per step to 30%. Without AMM, the same RWA tokens trade when bids cover asks, at their midpoint price. AMM quotes follow reserves instead of submitted prices; both variants share the volume reductions.
- **Payment default:** keep AMM and switch on-chain enforcement. Malicious buyers attempt nonpayment with probability 0.5. Enforcement prelocks 10% of initial buyer cash, recovers payment from collateral, adds a 10% trade-value penalty and excludes the defaulter; insufficient collateral rejects delivery. Without enforcement, unpaid delivery can occur and is not counted as successful allocation.

## Leasing experiment

The existing calibrated resource-release simulation uses 100 sellers, 200 buyers and 100 epochs, averaged over five service-order runs. Leases last 5–10 epochs before resources become available again. Reported cumulative satisfaction reaches 98.2% for leasing versus 70.4% for RWA purchase. This illustrates resource recirculation; satisfaction, resource utilization and net cash returns are different metrics.
