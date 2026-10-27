# Data Quality Assessment

## Overview

The dataset underwent an initial quality assessment before
modeling and analysis in Power BI. This document records the final
quality-control findings, analytical population definitions,
transformation decisions, and limitations of the completed Power BI report.

The assessment covered data completeness, key uniqueness,
referential integrity, categorical consistency, date validity,
and logical consistency.

## Identified Issues

| Issue | Affected Records | Status                                      |
|---|---:|---------------------------------------------|
| Performance reviews dated before hire | 1,141 | Confirmed inconsistency                     |
| Training taken exceeds opportunities offered | 823 | Requires clarification                      |
| Unmatched employee IDs in performance reviews | 0 | Passed                                      |
| Inconsistent tenure values | 0 | Passed                                      |
| Constrained self-rating and manager-rating differences | 6,708 of 6,709 reviews | Structural pattern - requires clarification |
## Source and Review Record Counts

| Measure | Count | Interpretation |
|---|---:|---|
| Employee source records | 1,470 | Unique employees in the full workforce |
| Original performance reviews | 6,709 | Review-level records, not employees |
| Reviews before employee hire dates | 1,141 | Flagged and excluded from review-based analysis |
| Chronologically eligible reviews | 5,568 | Reviews with `ReviewDate >= HireDate` |
| Selected latest eligible reviews | 1,217 | One per employee with an eligible review |
| Training consistency flags | 823 | Review records with taken > offered; variables excluded |
| Satisfaction fact rows | 4,868 | Four satisfaction aspects × 1,217 selected reviews |

**Important:** The 1,141 review chronology flags and the 823 training
consistency flags are separate checks that may overlap; the flagged
counts must not be added together. Chronology-excluded reviews are
retained in the raw/audit queries. Selecting 1,217 reviews from 5,568
eligible review records is a *latest-per-employee selection*, not an
additional set of invalid records.

## Data Cleaning

- Standardized categorical values using Power Query.
- Removed leading and trailing whitespace.
- Validated identifiers and lookup values.
- Identified chronological inconsistencies.
- Preserved original records for auditability.

## Analytical Decisions

- All 1,470 employee records are retained.
- Invalid review chronology is flagged rather than
  deleted from the source data.
- The most recent chronologically eligible review per employee is
  used for descriptive comparisons of satisfaction and performance
  by attrition status. These records are **not** treated as verified
  pre-departure assessments or causal explanations of departures.
- Both training variables are excluded from business analysis because
  their reference periods are unclear and the consistency check is flagged.
- Annual employee turnover cannot be calculated
  because termination dates are unavailable.

### Training Data Inconsistencies

The dataset contains 823 performance review records (12.3%)
where the number of training opportunities taken exceeds
the number of opportunities offered.

Although the number of offered training opportunities is
defined for the preceding 12 months, the reference period
for completed training is not clearly specified.

Consequently, it is not possible to determine whether
these discrepancies represent data quality issues or
differences in variable definitions.

**Analytical decision:**
Both training-related variables were excluded from the
business analysis to avoid potentially misleading conclusions.

The original data and audit results were retained for
documentation purposes.

## Analytical Limitations

The dataset does not provide employee termination dates
or a complete history of changes in employment conditions.

Consequently, the analysis focuses on cross-sectional
associations rather than causal relationships.

Additional results are documented in the dedicated discovery,
drivers-analysis, employee-experience and retention-strategy findings files.

Statistical validation was subsequently completed in Python, including hypothesis testing, effect-size estimation, 
multivariable logistic regression, model diagnostics, sensitivity analysis, and employee experience analysis.

## Analytical Populations and Review Coverage

| Status | Full workforce | Eligible-review cohort | Without eligible review | Coverage |
|---|---:|---:|---:|---:|
| Current employees (`Attrition = No`) | 1,233 | 993 | 240 | 80.5% |
| Leavers (`Attrition = Yes`) | 237 | 224 | 13 | 94.5% |
| **Total** | **1,470** | **1,217** | **253** | **82.8%** |

The recorded departure share equals **237 / 1,470 = 16.1%** in the full
workforce and **224 / 1,217 = 18.4%** among employees with eligible
reviews. Neither quantity is an annual turnover rate.

**253 employees** have no chronologically eligible performance review.
This may reflect the absence of any review or the absence of any review
dated on/after hiring; the split between those cases has not been
quantified here. These 253 employees remain part of the full-workforce
analyses and are excluded only from analyses requiring eligible ratings.

Review coverage is higher among leavers (94.5%) than among current
employees (80.5%), so the review cohort is not necessarily representative
of the full workforce. Differences can reflect selection effects.

### Main Analytical Tables

- `DimEmployee`: 1,470 unique employees; full-workforce comparisons.
- `FactLatestReview`: 1,217 latest eligible performance reviews; one per
  reviewed employee, including SelfRating and ManagerRating.
- `FactSatisfaction`: 4,868 aspect-level responses, four per reviewed
  employee; these are **not** 4,868 unique employees.
- `AI_AttritionDiscovery`: 1,217 unique reviewed employees, with
  workplace, compensation, satisfaction and rating fields combined
  for exploratory Power BI AI visualizations.
- Separate data-quality audit summary tables retain source-level checks;
  the What-if parameter table is intentionally disconnected.

## AI-Based Attrition Discovery

### Analytical Population

The exploratory AI analysis includes 1,217 employees
with at least one performance review dated on or after
their hire date.

This represents 82.8% of the employee dataset.

The analytical sample contains 224 employees recorded
as leavers and 993 employees recorded as current.

### Salary Assumption

Salary is treated as the latest recorded compensation
amount for each employee.

The dataset does not specify the currency, payment
period, or exact measurement date.

Salary is therefore included in exploratory
cross-sectional analysis but is not treated as
a verified pre-attrition predictor.

### Performance and Satisfaction Data

The most recent chronologically eligible performance
review was selected for each employee.

However, employee termination dates are unavailable.
Consequently, it cannot be confirmed that the selected
reviews preceded employee departures.

Associations involving satisfaction or performance
ratings must not be interpreted as causal effects
or validated predictors of attrition.

### Self-Rating and Manager-Rating Structure

An additional Python data-quality check identified a highly constrained relationship between `SelfRating` and `ManagerRating`.

Across all 6,709 original performance review records:

- 3,281 reviews have identical self- and manager ratings.
- 3,427 reviews have self-ratings exactly one point higher than manager ratings.
- Only 1 review has a manager rating one point higher than the self-rating.

Therefore, **6,708 of 6,709 reviews (99.99%) follow the same two patterns:** `SelfRating = ManagerRating` or `SelfRating = ManagerRating + 1`.

The pattern is also present in the latest eligible reviews selected for the 1,217-employee analytical cohort.

This highly regular structure may indicate a constraint in the rating process or the underlying data-generation methodology. However, its origin cannot be confirmed from the available documentation.

**Analytical decision:** The original ratings are retained without modification. Statistical agreement measures and paired comparisons are interpreted cautiously, as the observed differences may reflect the structure of the source data rather than independent employee and manager assessments.

The results must not be used as evidence that employees systematically overestimate their performance.

### Sample Selection

Employees without eligible performance reviews are
excluded from the AI discovery dataset.

Because review availability differs between leavers
and current employees, the analytical sample may
be affected by selection bias.

Key associations involving working conditions and salary were
subsequently compared with the full workforce (n = 1,470) on the
**Drivers Analysis** dashboard page. The AI-derived segments remained
associated with elevated recorded departure shares, although the
shares decreased when employees without eligible reviews were included.
This is an in-sample sensitivity check, **not** independent predictive
validation.
## Variable Inclusion and Exclusion Decisions

### Variables Used in Cross-Sectional Drivers Analysis

`OverTime`, `Department`, `JobRole`, `BusinessTravel`, `SalaryBand`,
`StockOptionCategory`, and `DistanceBand` are analyzed as recorded
employee characteristics. Satisfaction and performance ratings are
analyzed only where eligible reviews are available.

### Salary

Salary is interpreted as the latest recorded amount for each worker.
The source does not specify its currency, payment period or exact
measurement date. Salary bands are descriptive groupings of the
recorded amounts, not organizational pay grades. A salary value cannot
be verified as having been measured before an employee's departure.

### Age and Tenure-Related Variables

`Age`, `YearsAtCompany`, `YearsSinceLastPromotion`,
`YearsInMostRecentRole`, and `YearsWithCurrManager` were not selected as
drivers in this dashboard. Their reference time relative to departure
is ambiguous; some may also embed information about the end of
employment. Their exclusion is an analytical interpretability decision,
**not** evidence that the values failed numerical consistency checks.

### Training Variables

`TrainingOpportunitiesTaken` and `TrainingOpportunitiesWithinYear` were
excluded from business analysis because the period definitions are not
sufficiently comparable and 823 review records failed the direct
count comparison. The full review records were not removed on this
basis alone. No training-utilization rate is reported.

## Discovery, Verification and Retention-Scenario Boundaries

### AI Discovery and In-Sample Verification

Key Influencers and the Decomposition Tree were applied to the
eligible-review cohort (n = 1,217). The three discovered segments were
subsequently reproduced in the full workforce:

| Segment | Employees | Recorded leavers | Departure share |
|---|---:|---:|---:|
| Non-Tech, Overtime = Yes, Stock Option Level 0 | 67 | 38 | 56.7% |
| Technology, Overtime = Yes, Stock Option Level 0 | 115 | 44 | 38.3% |
| No Overtime, Salary below 45k, Stock Option Level 0 | 132 | 34 | 25.8% |
| Other employees | 1,156 | 121 | 10.5% |

The three non-overlapping priority segments contain **314 employees**
and **116 of the 237 recorded leavers (48.9%)**. They were defined using
observed associations in this dataset and should not be interpreted as
validated groups of future attrition risk. The 314 includes both
current employees and recorded leavers, not just staff currently
available for retention interventions.

### What-if Scenario

The Retention Strategy parameter is a **user-defined, hypothetical
percentage reduction in recorded departures within the priority
segments**, not an estimated effect of HR actions. The scenario
recalculates an illustrative count of fewer recorded departures and
its corresponding share of the currently filtered employee population.

For the unfiltered full workforce, a 10% scenario gives:

- 116 × 10% = 11.6, rounded to **12** illustrative fewer departures;
- 237 − 12 = **225** illustrative remaining leavers;
- 225 / 1,470 = **15.3%** illustrative departure share.

The scenario does not estimate future departures, annual turnover,
monetary savings, or the impact of any proposed intervention. Department
and Job Role filters change its underlying counts.

## Interpretation and Further Validation

The Power BI analysis identified descriptive associations between recorded attrition and selected workplace 
characteristics.

These findings were subsequently examined using statistical methods in Python, including hypothesis testing, 
effect-size estimation, confidence intervals, multivariable logistic regression, and model diagnostics.

Statistical analysis supported significant associations involving overtime, salary, selected stock option levels, 
and business travel. Employee satisfaction and performance ratings did not show statistically significant differences
by attrition status in the eligible-review cohort.

The findings remain observational. Missing termination dates and incomplete employment histories prevent confirmation
that recorded workplace characteristics preceded employee departures.

AI-discovered employee segments remain exploratory and have not been independently validated as predictions of future
attrition.

The complete statistical workflow is documented in notebooks/attrition_statistical_analysis.ipynb. The final 
business interpretation, key findings, and HR recommendations are presented in reports/employee_attrition_report.pdf.
