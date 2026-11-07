# RWA

Supplementary experiments for real-world asset integration in next-generation communication networks.

| PDF | Experiment |
| --- | --- |
| [Capital liquidity](capital_liquidity.pdf) | Time-dependent net cash returns under limited initial funding. |
| [Granularity self-ablation](ablation_allocation.pdf) | The reported RWA curve and two lower-token variants. |
| [Security self-ablation](ablation_robustness.pdf) | RWA with/without AMM pricing or on-chain payment enforcement. |
| [Leasing notes](Supplementary%20Notes%20for%20Leasing%20Mode.pdf), [leasing figure](leasing.pdf) | Existing resource-reuse and cumulative user-satisfaction experiment. |

## Capital liquidity

The firm needs 30% of a resource costing 100 normalized units. It starts with 10 units, accumulates 3 per epoch from existing business, and earns 5 per epoch once the required capacity is available. Leasing costs 3 per epoch; fractional purchase costs 30 and whole-block purchase costs 100. Unused whole-block capacity produces no extra income.

Returns deduct acquisition payments or recurring rent. Background savings determine purchase timing but are excluded from returns; residual asset value and rent-to-buy switching are also excluded. Purchase costs cause the downward jumps. Fractional and whole-block purchases start at epochs 6.67 and 30 and overtake leasing at 21.11 and 83.33. These are deterministic scenario results; lower rent or slower savings can move crossings beyond the observation window.

## RWA self-ablations

The new experiments extend the agents and constant-product pricing in `RWA.py`, with consistent inventory and payment accounting. There are 100 sellers with 1–5 resources each. New points average 10 paired seeds over 100 epochs; 95% bootstrap intervals are retained with the local results. Security bars display means without error bars, following the main figure's presentation. Physical supply, demand and cash budgets are shared within each comparison. Original pool/LP balances provide pricing reserves; only recorded seller inventory can be delivered.

**Granularity.** The blue curve retains the reported data from the paper's plotting source: 48%, 85%, 99%, 100%, 100% at 100–300 buyers. The other curves are new runs with 10 and 3 tokens per resource, versus the original code's 30-token setting. The initial whole-resource price remains 30, so initial token prices are 1, 3 and 10. Physical demand and buyer budgets are unchanged; coarse variants trade whole tokens. Local controls rerun the 30-token model both with and without integer lots.

The metric follows the original allocation driver: fully sold resource blocks divided by initial blocks, averaged over the last ten epochs. Liquidity providers number `max(20, buyers/2)`. Both coarse variants reach 100% in these settings; coarsening does not uniformly slow this metric. Large budgets and the whole-block completion criterion explain why a slower rise is not guaranteed. The reported curve is historical and allowed fractional token trades; it is not a fresh paired sample.

**Security.** All panels use 200 buyers, 100 liquidity providers, 30 tokens per resource and 0–30% malicious participants. The common metric is final **paid resource allocation / initial physical capacity**; unpaid occupancy is excluded.

- **Seller collusion:** compare full RWA with RWA without AMM. Malicious sellers raise asks by 1.2–1.5 times and reduce their listing rate to 30%; this slows release rather than permanently deleting capacity.
- **Buyer collusion:** compare the same AMM switch. Malicious buyers lower bids to 60–80% and spending per step to 30%. Without AMM, the same RWA tokens trade when bids cover asks, at their midpoint price. AMM quotes follow reserves instead of submitted prices; both variants share the volume reductions.
- **Payment default:** keep AMM and switch on-chain enforcement. Malicious buyers attempt nonpayment with probability 0.5. Enforcement prelocks 10% of initial buyer cash, recovers payment from collateral, adds a 10% trade-value penalty and excludes the defaulter; insufficient collateral rejects delivery. Without enforcement, unpaid delivery can occur and is not counted as successful allocation.

Detection and executable collateral are modeled assumptions, not a live-contract or consensus-security test. The curves identify component effects for these attacks and parameters.

## Leasing experiment

The existing calibrated resource-release simulation uses 100 sellers, 200 buyers and 100 epochs, averaged over five service-order runs. Leases last 5–10 epochs before resources become available again. Reported cumulative satisfaction reaches 98.2% for leasing versus 70.4% for RWA purchase. This illustrates resource recirculation; satisfaction, resource utilization and net cash returns are different metrics.
