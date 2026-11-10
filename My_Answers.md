# My Answers - Assignment 1 (CFLP: VNS vs Gurobi)

**Student Information:**
- **Student ID:** 447540249
- **Student Name:** Alanoud
- **Gurobi Version Used:** [x] Academic [ ] Free
- **Date Completed:** 10/11/2026

---

## Section A: Solution Quality Analysis (4 marks)

### A.1 (2 marks) - Gap Analysis by Categories

**Analysis of Plot 01:**

The median gap grew from 12.20% for small instances to 12.93% for medium and 14.03% for large. The Large-Moderate category had the biggest median gap among the nine groups, at 16.77%.

**Specific Observations:**
- Highest median gap size: Large
- Median gap value: 14%
- Effect of difficulty on gap: The median gap to Gurobi followed a consistent ordering at every problem size: Easy < Expensive < Moderate. VNS therefore performed best relative to Gurobi on Easy instances and worst on Moderate ones.

**Outliers identified:**
Plot 01 shows no unusual values. The worst gap, 24.70% on Large-Moderate instance 114, still sits inside its group’s whiskers.

**Interpretation:**
Larger instances give VNS more assignments to search through, making excellent solutions more difficult to locate. Moderate instances also have limited capacity, thus upgrading a solution may require relocating several clients at once. This probably explains their bigger median gaps.

---

### A.2 (2 marks) - Overall Solution Quality Statistics

**From Excel File (Sheet "All Results"):**

- Total instances analyzed: 144
- Instances with gap < 5%: 4 instances ||  4/144*100 = (2.77%)
- Instances with gap < 10%: 35 instances  ||  35/144*100 =  (24.30%)
- Mean gap across all instances: 13.37956481%
- Standard deviation of gap: 4.628260429%

**Interpretation:**
Over 144 instances, VNS solutions outperformed Gurobi by 13.38% on average, with a sample standard deviation of 4.63 percentage points and a range of 3.32% to 24.70%. This variation indicates the solution quality was inconsistent. Near-optimal results were rare. just four occurrences (2.78%) went below a 5% gap, 35 (24.31%) fell below 10%, and the other 109 exceeded 10%. As a result, In this experiment, VNS did not reliably approach Gurobi’s solution quality.


---

## Section B: Computational Efficiency Analysis (4 marks)

### B.1 (2 marks) - Time Comparison

**Analysis of Plot 02:**
**Size at which VNS becomes significantly faster:**
VNS becomes significantly faster at the large size, where its average time is about 0.82 s versus 5.21 s for Gurobi (about 6x faster).

**Most challenging configurations:**
- For VNS: large-expensive (size-difficulty) with time: 1.62 seconds
- For Gurobi: large-expensive (size-difficulty) with time: 12.75 seconds

**Detailed Comparison:**
Gurobi slows down significantly as problems become larger, reaching 12.75 s on large-expensive instances. VNS remains quick, requiring only 1.62 seconds on the same instances, which is about 8 times faster.
The only exception is in easy instances, when Gurobi is significantly faster (about 0.2 s vs. 0.3 s).
As a result, VNS is the preferable option when dealing with large or difficult problems. The deal-breaker is quality, its solutions are approximately 13.38% more expensive than Gurobi's.
---

### B.2 (2 marks) - Speedup Analysis

**Analysis of Plot 03:**

**Average speedup factors:**
- Small instances: 5.89x faster  [0.86 + 9.71 + 7.09/3= 5.886]
- Medium instances: 5.65x faster [0.78 + 11.75 + 4.43/3= 5.653]
- Large instances: 4.86x faster  [1.01 + 8.75 + 4.82/3= 4.86]

**Instances where Gurobi is faster (speedup < 1):**
Gurobi was faster (speedup < 1) in 39 of 144 instances (27%). Of these, 33 were Easy, 3 were Moderate and 3 were Expensive:
Easy, Small (11): 1, 3, 4, 7, 8, 9, 10, 12, 13, 15, 16
Easy, Medium (12): 49, 51, 52, 53, 54, 56, 57, 58, 59, 60, 61, 62
Easy, Large (10): 98, 99, 100, 101, 104, 105, 107, 108, 110, 111
Moderate (3): 28 (Small), 69 (Medium), 128 (Large)
Expensive (3): 42 and 48 (Small), 137 (Large)

**Practical Implications:**
VNS is most beneficial in real-life scenarios where a good solution is required rapidly, and a somewhat higher cost is acceptable.
In simple cases, Gurobi is the preferable option. It was faster in 33 out of 48 instances and returned the optimal solution, hence VNS has no benefit there.
In summary, VNS is best suited for fast decisions on complex problems, whereas Gurobi is best suited for scenarios when cost is important or the problem is simple.

---

## Section C: Scalability Analysis (3 marks)

### C.1 (1.5 marks) - Scalability Behavior

**Analysis of Plot 04:**

**VNS Scalability:**
VNS time increases gradually with problem size, from 0.33 s (small) to 0.42 s (medium) to 0.82 s (large) on average, with a maximum of about 4 s.

**Gurobi Scalability:**
Gurobi time increases quickly and varies significantly: 1.47 s, 2.39 s, and 5.21 s on average, with a maximum of almost 107 s. The majority of instances are still handled in less than one second, but a few hard ones take much longer.

**Comparison:**
VNS scales better. It is around 6 times quicker on average at large sizes and has far less variation since it does bound local search, whereas Gurobi must show optimality. However, VNS systems are around 13.38% more expensive.

---

### C.2 (1.5 marks) - Growth Rate and Predictions

**Observed Growth of Average Runtime (from your results):**

| | Small | Medium | Large | Small -> Medium (x) | Medium -> Large (x) |
|---|---|---|---|---|---|
| VNS avg time (s) |0.33|0.42|0.82|1.26x|1.97x|
| Gurobi avg time (s) |1.47|2.39|5.21|1.63x|2.18x|

**Shape of growth in Plot 04:**
- VNS: [ ] Roughly steady [x] Steadily increasing [ ] Sharply increasing
- Gurobi: [ ] Roughly steady [ ] Steadily increasing [x] Sharply increasing

**Justification:**
VNS grows by about 1.3x and then 2x per step, and its times stay below 1 s on average, so the growth is steady and moderate. Gurobi grows faster at every step (1.6x then 2.2x) and also has extreme outliers in the plot (up to about 107 s), so its growth is sharper and less predictable.

**Rough Prediction for Extra Large Instance (n=50, m=20):**
- Predicted VNS time: 1.61 seconds  || (0.81959 × 1.97=1.614)
- Predicted Gurobi time: 11.39 seconds || (5.21418 × 2.18447=11.390)
- How I computed it (e.g., applying the Medium -> Large ratio again): I multiplied each solver’s Large average by its Medium-to-Large growth ratio. 

**Suitability for Very Large Instances:**
I recommend using VNS for large problems when time is limited. Its runtime develops slower than Gurobi, and the expected difference expands to roughly 7 times at Extra Large (1.61s versus 11.39s).

---

## Section D: Quality-Time Tradeoff Analysis (3 marks)

### D.1 (1.5 marks) - Sweet Spot Identification

**Analysis of Plot 05:**

**Sweet Spot:**
VNS offered the best tradeoff on Medium–Expensive instances, which had the highest efficiency score (10.57). VNS took 0.61 seconds on average, compared with 6.05 seconds for Gurobi, but its solutions cost about 12% more. Plot 05 shows no clear pattern of smaller gaps at longer VNS runtimes.

**Time Savings for High-Quality Solutions (gap < 5%):**
- Average VNS time: 0.31 seconds
- Average Gurobi time: 0.09 seconds
- Absolute savings: -0.21 seconds
- Relative savings: -226%

**Interpretation:**
NS cannot deliver near-optimal cost and big time savings together. It suits hard problems where speed matters more than cost, and Gurobi suits easy problems or cases that need the best cost.

---

### D.2 (1.5 marks) - Practical Decision Making

**Scenarios Justifying 10-15% Gap:**

1. Unexpected warehouse closure ==> a higher-cost plan may be acceptable because the orders must be reassigned quickly.

2. Orders must be assigned before trucks leave ==> a higher-cost plan may be acceptable if it lets the trucks leave on schedule and avoids overtime.

3. A weekend sale needs extra storage ==> cost of 10–15% for two days may be worth it if the company can get the storage ready before the sale starts.

**Recommendation for Real-World Logistics Company:**

I recommend using both, depending on the situation: VNS for quick, recurring decisions and Gurobi when the lowest cost is needed.

---

## Section E: Algorithm Understanding (3 marks)

### E.1 (1.5 marks) - VNS Neighborhood Structures

**Role of Each Neighborhood:**

**N1 (Open Facility):**
- Purpose:open a closed facility to serve nearby clients more cheaply.
- Contribution: [ ] Intensification [x] Diversification
- Explanation: it changes which sites are used, moving the search to a new region.

**N2 (Close Facility):**
- Purpose: close an open facility and move its clients elsewhere to save its fixed cost.
- Contribution: [x] Intensification [ ] Diversification
- Explanation: it improves the current solution by removing underused facilities.

**N3 (Swap Facilities):**
- Purpose: close one facility and open another at the same time.
- Contribution: [ ] Intensification [x] Diversification
- Explanation: it is a bigger move that escapes local optima where opening or closing alone would raise the cost.

**N4 (Reassign Clients):**
- Purpose: move clients to a different open facility.
- Contribution: [x] Intensification [ ] Diversification
- Explanation: it fine-tunes assignments without changing which facilities are open.

**How They Complement Each Other:**

N1-N3 change which facilities are open, and N4 improves client assignments for that choice. When one neighborhood gets stuck, VNS switches to another, so the search escapes local optima and then refines the result.
---

### E.2 (1.5 marks) - Convergence Behavior Analysis

**Selected Convergence Plots:**

**Plot 1:** [Instance name: 124_cflp_large_moderate_fac22_cli66]
- Pattern: [ ] Smooth [x] Multiple jumps
- Description: cost drops in about 5 steps over 35 iterations, from about 26,800 to 25,900.
- What it reveals: VNS keeps finding improvements, but the final gap is still 22.4%.

**Plot 2:** [Instance name: 137_cflp_large_expensive_fac24_cli66]
- Pattern: [ ] Smooth [x] Multiple jumps
- Description: cost drops in 3 steps (iterations 4, 5 and 17), from about 25,350 to 24,800.
- What it reveals: improvements come early and once late, ending at a 14.2% gap.

**Plot 3:** [Instance name: 001_cflp_small_easy_fac17_cli64]
- Pattern: [x] Smooth [ ] Multiple jumps
- Description: the line is flat at about 16,460 for all 100 iterations.
- What it reveals: VNS got stuck in its first local optimum (9.1% gap) and never improved.

**Role of Shaking Mechanism:**
Shaking perturbs the current solution so local search can leave a local optimum. In Plots 1 and 2, the step drops after flat periods are where shaking found a better solution. In Plot 3, it found none. Even so, every final cost stays above Gurobi’s optimum, so shaking helps but does not close the gap.
---

## Section F: Critical Reflection (3 marks)

### F.1 (1 mark) - Limitations and Improvements

**Main Limitations of Current VNS Implementation:**

1. Large gap to optimal: 13.38% on average, and only 4 of 144 instances are below 5%.

2. Gets stuck early: 102 of 144 instances never improved after the first solution.

3. No quality guarantee, and it is weakest on tight-capacity Moderate instances.

**Suggested Improvements:**

1. Stronger shaking and more neighborhoods (moving several clients or facilities together) to escape local optima, especially under tight capacity.
2. Better starting solution (greedy or LP-based) so the search does not start in a poor region.

3. Multiple restarts, or VNS as a warm start for Gurobi, using VNS’s spare time (under 1 s) to close part of the gap.]

---

### F.2 (1 mark) - Real-World Deployment Considerations

**Additional Constraints for Real Logistics Company:**

1. Delivery time windows and driver working hours: Plans must meet customer deadlines, or they cannot be used.

2. Vehicle fleet size and routing costs: Real costs depend on routes, not only on facility-client assignment.

3. Uncertain demand and capacity changes (ex: demand spikes or a warehouse closure): Plans must be robust and quick to re-solve.

**Additional Objectives:**
Beyond cost, the business is concerned with service level (on-time delivery), balanced workload across facilities, disruption resilience, and reduced emissions. These are in conflict with cost; thus the optimum option is a trade-off.

---

### F.3 (1 mark) - Exact Method vs Heuristic in Practice

**Gurobi Optimality Status (from the `gurobi_status` column):**
- Instances solved to proven optimality: 144 out of 144
- Instances stopped at the time limit: 0 out of 144
- Do the time-limit instances share a size/difficulty?? No, there are none. Gurobi proved optimality on every instance. Its slowest run was about 107s, so all were finished.

**What VNS Gives Up and What It Gains:**
VNS gives up 13.38% in cost on average. In return it saves about 2.5 s per instance (3.02 s vs 0.52 s), roughly 83% of Gurobi’s total time. The saving comes mostly from hard instances.

**Practical Value of Heuristics:**
Gurobi solved everything here, but its time grows faster and has long tails (up to 107 s). VNS-like heuristics give fast, predictable answers, which matters for re-planning, testing many scenarios and very large problems. The cost is the 13.38% gap, so they suit cases where speed matters more than the best cost.
---

## Section G: BONUS - VNS Improvement Challenge (+3 marks, optional)

*Leave this section empty if you do not attempt the bonus. See Section 8 of the guide. Your improved notebook (`StudentID_FirstName_LastName_Assignment1_IMPROVED.ipynb`) must be pushed to your repository.*

### G.1 (1 mark) - Bug Identification

**Where is the bug?** (cell / function / line numbers in `Assignment_1.ipynb`):

[Paste the faulty line(s) of code]

**What does the bug do?**

[Describe the specific issue]

**Why does it degrade VNS performance?**

[Explain the effect on the search and link it to the high gaps (>20%) in your results]

---

### G.2 (1 mark) - The Fix

**Corrected code:**

```python
# paste your fixed line(s) here
```

**Why does the fix work and why does it not break the rest of the algorithm?**

[Explanation]

---

### G.3 (1 mark) - Demonstrated Improvement

**Before vs After (same instances):**

| Metric | Original VNS | Improved VNS |
|---|---|---|
| Mean gap (%) | | |
| Std of gap (%) | | |
| Instances with gap < 5% | | |
| Instances with gap > 20% | | |
| Mean VNS time (s) | | |

**Analysis:**

[Discuss the improvement, and any change in running time]

**Improved results files (names in your repository):** ___________

---

## Additional Comments (Optional)

[Any additional observations, challenges faced, or insights gained]

---

## Declaration

I hereby declare that:
- I have completed this assignment independently
- All numerical results are from MY experiments using MY student ID
- All analysis and interpretations are MY own work
- I have not copied results or answers from other students
- I understand the consequences of academic dishonesty

**Signature:** Alanoud Aljohani

**Date:** 10/11/2026

---

**END OF MY ANSWERS**
