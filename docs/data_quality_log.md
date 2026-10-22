# Data Quality Assessment

## Overview

The dataset underwent an initial quality assessment before
data modeling and analysis in Power BI.

The assessment covered data completeness, key uniqueness,
referential integrity, categorical consistency, date validity,
and logical consistency.

## Identified Issues

| Issue | Affected Records | Status |
|---|---:|---|
| Performance reviews dated before hire | 1,141 | Confirmed inconsistency |
| Training taken exceeds opportunities offered | 823 | Requires clarification |
| Unmatched employee IDs in performance reviews | 0 | Passed |
| Inconsistent tenure values | 0 | Passed |

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
- Historical performance reviews will not be used
  to explain employee departures.
- Training utilization metrics are excluded pending
  clarification of variable definitions.
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

Additional data quality checks and methodological
decisions will be documented as the project progresses.

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

### Sample Selection

Employees without eligible performance reviews are
excluded from the AI discovery dataset.

Because review availability differs between leavers
and current employees, the analytical sample may
be affected by selection bias.

Key associations involving workplace conditions
and salary will be compared against the full
employee dataset during subsequent analysis.