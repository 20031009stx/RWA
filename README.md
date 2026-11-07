# RWA
Leasing mode for real-world asset integration in next-generation communication networks.

## Supplementary experiments

| Figure | What it examines |
| --- | --- |
| [Capital liquidity](capital_liquidity.pdf) | Cumulative net cash return over time: leasing, RWA fractional purchase, and direct whole-block purchase. |
| [Allocation ablation](ablation_allocation.pdf) | Allocation granularity, pricing, and coupled funding/initial-price sensitivity. |
| [Robustness ablation](ablation_robustness.pdf) | Supply withholding, buyer limit-price reduction, and settlement protection. |

### Capital liquidity: time and cash returns

This single-panel figure is a deterministic firm cash-flow scenario. A whole resource costs 100 normalized units; the firm requires 30% of it, starts with 10 units, and accumulates 3 units per epoch from its existing business. Once access starts, the required capacity generates 5 units per epoch before access costs. Leasing costs 3 units per epoch; RWA fractional purchase costs 30; whole-block purchase costs 100. Unused whole-block capacity generates no additional revenue.

The plotted return is resource-generated operating cash minus purchase outlays or recurring rent. Background savings determine affordability but are excluded from returns. A downward purchase jump is the full acquisition payment, not a negative company cash balance. The strategies do not switch between renting and buying; asset residual values, resale and token appreciation are excluded.

In this scenario, fractional and whole-block purchases start at epochs 6.67 and 30, and overtake leasing at 21.11 and 83.33. Leasing helps early access; fractional purchase reduces the funding delay; recurring rent can outweigh purchasing over a sufficiently long horizon. These are conditional cash-flow results, not market-calibrated return forecasts. Lower rent or slower capital accumulation can delay the intersections beyond the observation window.

### What "Ask-price matching" means

Previously labeled "Quote", this is a simplified mechanism replacement for AMM pricing. Buyers are processed in a shared arrival order; sellers are considered from lowest to highest ask. Trades respect available inventory, lot size, buyer budgets and the value of the requested bandwidth. It is not MPRA, TRA, CPA, or a new named auction algorithm.

The AMM instead prices trades using a finite constant-product pool. Both mechanisms receive the same real inventory and initial cash; matching leaves that cash idle. Sellers precommit offered inventory. These are controlled component variants, not reproductions of the paper's complete implementations.

### Reading the ablation figures

These two figures use 100 sellers, 100–300 buyers (200 in attack tests), 30 paired seeds and 95% bootstrap confidence intervals. All variants share physical supply, demand, budgets and attack identities. A block is 10 MHz; fine allocation uses 0.1 MHz slices.

- **Allocation (a):** compare coarse and fine lots within each mechanism. Demand-serving utilization counts allocated bandwidth up to each buyer's actual need; excess whole-block capacity is excluded.
- **Allocation (b):** show the fine-lot gain within each mechanism, the AMM-minus-matching difference at the same fine granularity, and their interaction (the difference between fine-lot gains). The measured interaction does not support positive integration synergy in this model.
- **Allocation (c):** vary initial cash while keeping inventory and buyer budgets fixed. This changes the AMM's initial price as well as funding, so it is not an isolated liquidity-depth test.
- **Robustness (a):** malicious sellers withhold 70% of their coalition's supply, rounded to whole blocks; initial cash remains fixed.
- **Robustness (b):** malicious buyers reduce their limit prices to 70%. A flat curve means the remaining demand can still absorb supply in this scenario, not immunity to arbitrary collusion.
- **Robustness (c):** malicious buyers attempt nonpayment with probability 0.5. Settlement-on rejects unpaid delivery; settlement-off permits it. Paid demand-serving utilization excludes unpaid allocation and distinguishes successful exchange from resource occupancy.

The ablations identify component effects under the modeled conditions; they do not establish universal integration gains, live-contract security, or secondary-market resale liquidity.
