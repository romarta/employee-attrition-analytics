# Employee Attrition & Retention Analytics

> **Project status:** Power BI dashboard complete (6 pages). Python statistical validation and the Quarto PDF report are the next phases.

An end-to-end HR analytics portfolio project examining **where employee departures are concentrated**, **which recorded employee characteristics are associated with departures**, and **where HR could focus further investigation**. The project combines Power BI data modeling and interactive analysis with documented data-quality decisions; independent statistical validation and a reproducible written report are planned.

## Business Questions

- Where are recorded employee departures concentrated across departments and job roles?
- Which workplace, compensation, and employee-experience characteristics are associated with attrition status?
- Do exploratory patterns persist when compared with the full workforce?
- Which employee segments warrant further investigation, and what could illustrative scenarios imply?
- How do data quality and missing dates limit interpretation?

## Power BI Dashboard — Completed

[View the interactive Power BI dashboard](https://app.powerbi.com/view?r=eyJrIjoiNDI2NDQ1ZGUtZjU5Mi00YzQ3LWIxYjItYjIxYzc0NTk5ZTY4IiwidCI6IjJmYWI1MTA4LTBiM2UtNDYwMy05Yjc3LTM2Y2QyYzk0ZmEzZSJ9)

The interactive report contains **six pages**, built with Power Query, DAX measures organized in `_Measures`, and a consistent navigation and filter layout.

| Page | Business question | Main analysis |
|---|---|---|
| **Executive Overview** | Where are employee departures concentrated across the organization? | Workforce KPIs and departures by department and job role. |
| **Drivers Discovery** | Which factors are most strongly associated with employee attrition? | Key Influencers and Decomposition Tree; bookmark-based exploration on the eligible-review cohort. |
| **Drivers Analysis** | Do the AI-discovered attrition patterns hold across the workforce? | Overtime, salary-band and stock-option comparisons; department breakdowns; in-sample segment checks against the full workforce. |
| **Employee Experience** | How do satisfaction and performance ratings differ between current employees and leavers? | Satisfaction averages and ordinal rating distributions, including self- and manager ratings. |
| **Retention Strategy** | Where should HR prioritize retention efforts, and what could different scenarios imply? | Priority segments, investigation recommendations, and a clearly labeled illustrative What-if calculation. |
| **Data & Methodology** | How reliable are the data, and what are the analytical limitations? | Quality audit, review coverage, population selection, transformations, and interpretation boundaries. |

## Data and Analytical Populations

The dataset consists of `Employee` (1,470 employee records), `PerformanceRating` (6,709 review records), and three lookup tables: `EducationLevel`, `RatingLevel`, and `SatisfiedLevel`.

| Metric | Full workforce | Eligible-review cohort |
|---|---:|---:|
| Employees | 1,470 | 1,217 |
| Current employees (`Attrition = No`) | 1,233 | 993 |
| Recorded leavers (`Attrition = Yes`) | 237 | 224 |
| Recorded departure share | **16.1%** | **18.4%** |

The **full workforce** is used for organizational and employment-condition comparisons. The **eligible-review cohort** includes only employees with at least one review dated on or after their hire date; the latest such review was selected for each employee. It is used for satisfaction, performance, and AI exploration. The remaining **253 employees are retained** in full-workforce analyses, but cannot be included in analyses requiring eligible ratings.

*Recorded departure share is the number of employees marked as leavers divided by the relevant population. It is **not** an annual turnover rate.*

## Selected Findings

These are descriptive findings from the completed Power BI dashboard, **not causal effects or validated predictions**.

| Area | Observed result |
|---|---|
| **Overtime** | The recorded departure share is **30.5%** for employees with overtime versus **10.4%** for those without. The difference appears in all three departments. |
| **Compensation** | The recorded departure share ranges from **26.6%** in the lowest salary band (`Below 45k`) to **9.2%** in the highest band (`150k+`). Salary is the latest recorded amount; its currency, payment period, and measurement date are unspecified. |
| **Stock options** | `Level 0` has a **24.4%** recorded departure share; the pattern across levels is **not monotonic**. |
| **Priority segments** | Three exploratory segments contain **314 of 1,470 employees (21.4%)** and **116 of 237 recorded leavers (48.9%)**. These were identified in-sample and are groups for further investigation, not a prospective risk model. |
| **Employee experience** | In the eligible-review cohort, average Work-Life Balance is **3.40** for current employees versus **3.27** for leavers. Self- and manager-rating averages differ only slightly between the groups. |

The retention What-if feature allows a **user-defined hypothetical percentage reduction** to be applied to the 116 recorded departures in the three priority segments (before any filters). For example, a 10% assumption produces an illustrative difference of 12 departures and an illustrative overall recorded departure share of **15.3%**. This is **an arithmetic sensitivity scenario, not a forecast or an estimated intervention effect**.

## Data Quality and Methodological Decisions

A documented Power Query audit identified:

- **1,141 reviews (17.0%)** dated before the employee's hire date. These remain available for audit but were excluded from review-based analysis; **5,568** reviews satisfy `ReviewDate >= HireDate`.
- **823 review records (12.3%)** where training opportunities taken exceed opportunities indicated as available. As the definitions/reference periods are unclear, **both training variables were excluded from business analysis**; the affected records were not removed solely for this reason.
- **1,217 latest eligible reviews**, one per employee, producing **4,868 satisfaction-aspect rows** (four aspects per reviewed employee).
- **Uneven review coverage:** 80.5% among current employees versus 94.5% among leavers, creating potential selection bias.

Additional boundaries apply throughout the report:

- **No termination dates:** review timing cannot be verified as pre-departure, and annual employee turnover cannot be calculated.
- **No complete historical snapshots:** salary and selected age/tenure-related fields lack a clear point-in-time reference relative to departures. These limitations shaped variable selection and interpretation.
- **Ordinal ratings:** satisfaction and performance averages are supplemented with response distributions; differences are descriptive pending statistical validation.
- **AI discovery and What-if:** Key Influencers, Decomposition Tree, segment comparisons, and scenarios support exploration and prioritization—not causal attribution, individual risk scoring, or intervention-effect forecasts.

See [Data Quality Assessment](docs/data_quality_log.md) for the detailed audit, exclusions, and population definitions.

## Tools and Project Structure

**Completed:** Power BI Desktop, Power Query, data modeling, DAX, Key Influencers, Decomposition Tree, bookmarks, and What-if parameters. All authored DAX measures are organized in the `_Measures` table.

**Upcoming:** Python for independent numerical and statistical checks; Quarto for a reproducible PDF report.

```text
employee-attrition-analytics/
├── README.md
├── powerbi/                # Power BI report (.pbix)
└── docs/
    ├── data_quality_log.md
    ├── employee_experience_findings.md
    └── retention_strategy_findings.md
```

The tree highlights the main documentation files discussed in this project; other source and supporting files may also be present. Open the `.pbix` file in Power BI Desktop to explore the interactive report. This repository README will be expanded with reproducible Python outputs and the Quarto report when those stages are complete.

## Next Steps

1. **Python validation:** reproduce core Power BI counts and rates; assess uncertainty and effect sizes; investigate potential confounding by department and job role.
2. **Quarto PDF report:** consolidate methods, data-quality decisions, validated findings, interpretation limits, and proposed HR investigations.
3. **Portfolio polish:** add a dashboard preview and links to the final report and reproducible analysis artifacts.

> **Interpretation note:** The source data are cross-sectional. Reported attrition percentages describe the proportion of records marked as leavers; observed associations do not establish why employees left.
