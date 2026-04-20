# supply-chain-network-design
Mixed-Integer Linear Programming (MILP) model for optimizing a multi-echelon supply chain network, featuring automated sensitivity analysis using Python and Gurobi.

### The Business Problem
A manufacturing entity operates two main factories (with maximum supply capacities) and serves six distinct customer markets (with known demands). The product must be routed through a set of intermediate depots. 

**Key Decisions to Optimize:**
1. Which exactly four of the six available depots should be opened?
2. Should the existing capacity of the Birmingham depot be expanded for an additional fixed cost?
3. What is the optimal flow of goods from factories $\rightarrow$ depots $\rightarrow$ customers to minimize total network costs?

## Mathematical Formulation:
**Objective Function:** 
- Minimize the sum of variable shipping costs, fixed depot opening costs, and discrete expansion costs.

**Constraints:**
- Strict flow conservation at intermediate depots.
- Factory production limits and capacitated depot throughputs.
- Exact satisfaction of end-customer demand.
- Cardinality limit restricting the network to exactly 4 open depots.

## Sensitivity Analysis
Optimization models must be resilient to real-world volatility. This project includes parametric sweeps to test the network's structural response to:
- **Transport Cost Multipliers:** Scaling shipping costs by factors (e.g., 0.9x to 1.2x) to observe shifts in optimal routing.
- **Expansion Cost Sweeps:** Varying the fixed cost of expanding the Birmingham depot (from \$2,000 to \$8,000) to find the breakeven threshold where expansion is no longer economically viable.
- **Demand Scaling:** Stress-testing the network by simulating market contractions (0.8x) and surges (1.2x) to ensure capacity limits are not breached.

## Key Findings & Results
The MILP model successfully identified the lowest-cost supply network configuration, balancing fixed facility costs against variable transportation routes. 

**Baseline Optimal Solution:**
- **Total Network Cost:** $174,000
- **Selected Depots:** London, Exeter, Northampton, and Birmingham (with Newcastle and Bristol remaining closed).
- **Capacity Expansion:** The model recommended expanding the Birmingham depot's capacity to accommodate optimal routing from the Brighton factory.

**Strategic Insights from Sensitivity Analysis:**
- **Expansion Cost Threshold:** Expanding the Birmingham depot remains the optimal structural choice until the expansion cost reaches **$5,000**. Beyond this threshold, the solver automatically re-routes the flow, bypassing the expansion and absorbing higher transportation costs ($181,000) instead.
- **Network Robustness:** The chosen depot configuration (London, Exeter, Northampton, Birmingham) remained structurally optimal even when customer demand scaled up by 20% and down by 20%, proving the network design is highly resilient to market volatility.
