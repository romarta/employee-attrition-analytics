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