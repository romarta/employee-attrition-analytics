# Retention Strategy - Findings and Recommendations

## 1. Business Objective

**Business question:** Where should HR prioritize retention efforts, and what could different scenarios imply?

This page translates the project's descriptive attrition findings into priorities for **further HR investigation** and an illustrative What-if scenario. It does **not** estimate the causal impact of an intervention, predict future departures, or calculate an annual turnover rate.

## 2. Analytical Population and Definitions

The Retention Strategy page uses the **full workforce of 1,470 employees**, rather than the 1,217-person eligible-review cohort used for parts of Drivers Discovery and Employee Experience.

| Measure | Full workforce |
|---|---:|
| Employees | 1,470 |
| Current employees | 1,233 |
| Recorded leavers | 237 |
| Attrition share | 16.1% |

**Attrition share** is the number of employees recorded as leavers divided by the total number of employees in the dataset. As termination dates and a defined observation period are unavailable, it is **not an annual attrition/turnover rate**.

The three priority segments were initially identified in Power BI Key Influencers (*Top Segments*) on the eligible-review cohort and then reconstructed using observed employee characteristics for the full workforce. These segments were **not independently validated on an external dataset**.

## 3. Priority Segment Definitions

Segments are mutually exclusive and assign each employee to one category.

| Segment | Definition |
|---|---|
| Non-Tech, OT, Stock 0 | `Department <> Technology`, `OverTime = Yes`, `StockOptionLevel = 0` |
| Tech, OT, Stock 0 | `Department = Technology`, `OverTime = Yes`, `StockOptionLevel = 0` |
| No OT, Low Salary, Stock 0 | `OverTime = No`, `Salary < 45,000`, `StockOptionLevel = 0` |
| Other Employees | All employees not meeting any of the three definitions |

`Salary` is assumed to be the latest recorded employee compensation amount. Its currency, pay period, measurement date, and history are unknown. The threshold of 45,000 is an analytical grouping, **not** an independently validated compensation benchmark.

## 4. Observed Concentration of Departures

### Full-workforce results

| Segment | Employees | Leavers | Current employees | Attrition share |
|---|---:|---:|---:|---:|
| Non-Tech, OT, Stock 0 | 67 | 38 | 29 | 56.7% |
| Tech, OT, Stock 0 | 115 | 44 | 71 | 38.3% |
| No OT, Low Salary, Stock 0 | 132 | 34 | 98 | 25.8% |
| Other Employees | 1,156 | 121 | 1,035 | 10.5% |
| **Total** | **1,470** | **237** | **1,233** | **16.1%** |

The first three groups contain:

- **314 employees**, equivalent to **21.4%** of the full dataset;
- **116 recorded leavers**, equivalent to **48.9%** of all recorded departures;
- **198 current employees** represented in the same descriptively defined groups.

**Finding:** Recorded departures are concentrated in three comparatively small, AI-discovered groups. These are *investigation priorities*, not validated individual risk classifications. The 198 currently employed people in these groups must not be described as likely to leave or as automatically requiring intervention.

### Reviewed cohort vs. full workforce

| Priority segment | Eligible-review cohort: employees | Eligible-review cohort: leavers | Eligible-review attrition share | Full-workforce attrition share |
|---|---:|---:|---:|---:|
| Non-Tech, OT, Stock 0 | 62 | 38 | 61.3% | 56.7% |
| Tech, OT, Stock 0 | 99 | 43 | 43.4% | 38.3% |
| No OT, Low Salary, Stock 0 | 96 | 30 | 31.3% | 25.8% |

The higher shares in the eligible-review cohort illustrate the importance of **review-coverage selection**. Reproducing these patterns in the full dataset provides a useful descriptive check, but it does not constitute out-of-sample or predictive validation.

## 5. Evidence Informing Retention Priorities

### Overtime

In the full workforce, attrition share is **30.5%** among employees with `OverTime = Yes`, compared with **10.4%** among employees with `OverTime = No`. The overtime group has a higher observed share in all three departments.

### Compensation

Attrition share by latest-recorded salary band:

| Salary band | Attrition share |
|---|---:|
| Below 45k | 26.6% |
| 45k–75k | 14.6% |
| 75k–150k | 12.9% |
| 150k+ | 9.2% |

These are unadjusted, cross-sectional comparisons. Role composition and other workforce characteristics may explain part of the pattern.

### Stock options

| Stock option level | Attrition share |
|---|---:|
| Level 0 | 24.4% |
| Level 1 | 9.4% |
| Level 2 | 7.6% |
| Level 3 | 17.6% |

Level 0 has the highest observed share, but the pattern across levels is **not monotonic**. These categories must not be interpreted as evidence that each increment in stock options causes a reduction in departures.

### Employee experience

Within the eligible-review cohort, mean Work-Life Balance is **3.40** for current employees and **3.27** for leavers, a descriptive difference of **−0.13** rating points (leavers minus current employees). This is a modest difference, and the latest eligible reviews are **not verified as having occurred before departure**.

## 6. Recommended HR Investigations

The recommendations below propose **diagnostic next steps**. They are not claims of demonstrated intervention effectiveness.

| Priority | Area | Evidence | Proposed action | Example monitoring measures |
|---|---|---|---|---|
| 1 | **Workload & Scheduling Review** | Higher attrition share among employees with overtime across departments; modest Work-Life Balance differences in the reviewed cohort | Audit overtime frequency, staffing capacity, scheduling practices and workload distribution; collect voluntary employee feedback before changing policies | Overtime hours, staffing gaps, employee feedback, subsequent departures measured over a defined period |
| 2 | **Compensation & Rewards Review** | Elevated attrition share in the lowest salary band and among Stock Option Level 0 employees | Assess compensation competitiveness **within comparable roles** and review reward eligibility, policies and equity; avoid automatic blanket adjustments based on these correlations | Role-adjusted pay comparisons, reward eligibility, feedback, subsequent departures |
| 3 | **Targeted Employee Listening** | Three observed segments contain 48.9% of departures but 21.4% of employees | Use confidential stay interviews and anonymous pulse surveys; investigate reported issues before selecting interventions | Participation, qualitative themes, survey trends and prospective retention outcomes |

Any application to current employees should respect confidentiality, fairness and employment-law requirements. Segment membership is not an individual prediction and should not be used as the sole basis for personnel decisions.

## 7. Illustrative What-if Scenario

### 7.1. Definition

**Input: Hypothetical Reduction in Priority Segment Departures (%).**

The user enters a percentage from **0 to 30**, where, for example, the number `10` means **10%**, not a decimal `0.10` or a ten-percentage-point change in overall attrition share.

The reduction is applied **only to recorded leavers in the three priority segments**. In the unfiltered dataset, the base is **116 recorded priority-segment departures**, not 237 organization-wide departures or 314 segment members.

### 7.2. Calculation

For the current Department and Job Role filter context:

1. **Illustrative fewer leavers** = `ROUND(Priority Leavers × Assumed Reduction / 100, 0)`.
2. **Illustrative remaining leavers** = `Observed Leavers − Illustrative Fewer Leavers`.
3. **Illustrative attrition share** = `Illustrative Remaining Leavers / Employees`.

The denominator remains the observed employee count for the selected workforce; the exercise is a **static counterfactual arithmetic illustration**. Whole-person counts are rounded, so changes need not be perfectly smooth at every one-percentage-point increment.

### 7.3. Example results: no workforce filters

| User input: assumed reduction | Illustrative fewer leavers | Illustrative remaining leavers | Illustrative attrition share |
|---|---:|---:|---:|
| 0% | 0 | 237 | 16.1% |
| 5% | 6 | 231 | 15.7% |
| **10%** | **12** | **225** | **15.3%** |
| 15% | 17 | 220 | 15.0% |
| 20% | 23 | 214 | 14.6% |
| 25% | 29 | 208 | 14.1% |
| 30% | 35 | 202 | 13.7% |

At 10%, for example: `116 × 0.10 = 11.6`, rounded to **12**; `237 − 12 = 225`; `225 / 1,470 = 15.3%`.

Department and Job Role selections change the observed population, priority-segment leavers and hypothetical scenario outputs. Therefore the 116-person base applies **only when filters are cleared**.

### 7.4. Interpretation boundaries

The input percentages are **user-defined assumptions** and have **not** been estimated from interventions, experiments or historical response data. The scenario does not:

- forecast future attrition;
- estimate preventable departures or causal treatment effects;
- estimate annual turnover;
- calculate cost savings or financial ROI;
- establish that any proposed HR action could achieve the chosen percentage.

The chart/card title **Illustrative Attrition Share** must not be replaced with *predicted attrition rate*.

## 8. Data and Methodological Limitations

1. **Missing termination dates:** departures cannot be assigned to a reporting period, so the observed attrition share is not annualized.
2. **Unknown measurement times:** overtime, compensation, rewards and other snapshot fields are not verified pre-exit measures for leavers.
3. **Reviewed-cohort bias:** Key Influencers was initially run on 1,217 employees with chronologically eligible reviews, while retention priorities are presented for all 1,470 employees.
4. **Unverified review timing:** review dates were checked against hire dates, not unavailable termination dates. Satisfaction comparisons may include ratings whose relationship to departure timing is unknown.
5. **Data-driven segment selection:** priority groups were discovered using the analyzed dataset; their elevated shares may reflect selection effects and overfitting.
6. **Confounding:** job role, pay, stock options and overtime may be interrelated. The descriptive results do not establish independent causal contributions.
7. **No intervention outcomes:** the What-if input has no empirically established efficacy and is not suitable for prediction.
8. **Training data exclusion:** training opportunity fields were excluded from business analysis because of inconsistent or ambiguous definitions, as recorded in the data quality log.

## 9. Next Validation Steps

At the Python and Quarto reporting stage:

1. Recompute full-population and segment-level counts directly from the curated data.
2. Report uncertainty intervals for group-level attrition shares and differences.
3. Examine salary, job role, department, stock options and overtime jointly to assess confounding and sparse categories.
4. Compare findings across full and eligible-review populations, clearly distinguishing the samples.
5. Evaluate satisfaction differences using ordinal-appropriate methods, sample sizes and effect sizes.
6. Specify what additional longitudinal data and prospective evaluation would be required to estimate actual intervention impact.

## 10. Report Reference and Status

- **Report:** Employee Attrition & Retention Analytics
- **Dashboard page:** Retention Strategy
- **Main source table:** `DimEmployee`
- **Measures table:** `_Measures` / `05 | Retention Strategy`
- **Scenario parameter table:** `Scenario Reduction` (disconnected)
- **Population:** Full workforce, n = 1,470 (before filtering)
- **Analysis type:** Descriptive priority setting and hypothetical scenario arithmetic
- **Status:** Power BI results visually checked for the unfiltered 0% and 10% scenarios; statistical and causal validation not performed
