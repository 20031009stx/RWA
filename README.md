# RWA
Leasing mode for real-world asset integration in next-generation communication networks.

## Supplementary experiments

| Figure | What it examines |
| --- | --- |
| [Capital liquidity](capital_liquidity.png) | Upfront funding and budget-feasible access: whole-block purchase, fractional purchase, and short-term lease. |
| [Allocation ablation](ablation_allocation.png) | Coarse/fine allocation under AMM pricing or quote-based matching, with funding sensitivity. |
| [Robustness ablation](ablation_robustness.png) | Supply withholding, reduced buyer limit prices, and payment default, including settlement protection on/off. |

Results use 30 paired random seeds and 95% bootstrap confidence intervals. There are 100 sellers, 100–300 buyers (200 for funding and attack tests), and 10 MHz blocks divisible into 0.1 MHz slices. Physical supply, demand, and budgets are shared across variants within each comparison.

**Funding.** The purchase price per block is normalized to 1. Reference leases last 5–10 epochs: rent is purchase value/100 per epoch, plus a 10% refundable deposit. Budgets equal requested fractional purchase value × budget scale × U(0.5, 1.5). Rent and deposit sensitivity is included. These are scenario assumptions; affordability precedes matching, and upfront cash is not total economic cost.

**Ablations.** Sellers precommit inventory. AMM uses reserve-based prices; matching uses seller asks. Both receive the same real stock and initial cash (held idle by matching), with funding fixed across attacks. Demand-serving utilization excludes excess allocation; paid utilization also excludes unpaid delivery. These are controlled mechanism variants, not reproductions of the paper's named baselines.

The results identify component effects under the modeled conditions. They do not establish universal integration gains or secondary-market resale liquidity.
