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

**Completed — Power BI:** Power BI Desktop, Power Query, data modeling, DAX, Key Influencers, Decomposition Tree, bookmarks, and What-if parameters. The interactive dashboard consists of six completed pages. All authored DAX measures are organized in the `_Measures` table.

**In Progress — Python Statistical Analysis:** JupyterLab, pandas, NumPy, SciPy, statsmodels, Seaborn, and Matplotlib. The analysis includes statistical hypothesis testing, effect sizes, confidence intervals, bootstrap methods, and visualizations. Data preparation and statistical analyses of overtime and salary have been completed. Further analyses will examine stock options, department-level differences, multivariable logistic regression, and employee experience.

**Upcoming — Quarto PDF Report:** A reproducible analytical report combining Power BI findings, Python statistical results, data-quality considerations, visualizations, and HR recommendations.

### Project Structure

```text
employee-attrition-analytics/
│
├── README.md
├── datasets/
│   ├── processed/              # Prepared analytical datasets
│   └── ...                     # Original source datasets
│
├── docs/                       # Data quality and analytical findings
│
├── notebooks/
│   └── attrition_statistical_analysis.ipynb
│
├── powerbi/
│   ├── screenshots/            # AI visual previews and data model
│   ├── themes/                 # Power BI theme configuration
│   └── employee_attrition_analytics.pbix
│
└── reports/                    # Quarto PDF report (upcoming)
```
```

The Jupyter notebook contains the statistical analysis workflow, including data preparation, hypothesis testing, effect size estimation, and Seaborn visualizations.

The final Quarto report will be added after completing the statistical analysis.
## Next Steps

1. **Python statistical analysis (in progress):**
   - **Completed:** Data preparation, statistical analysis of overtime and salary, effect sizes, confidence intervals, and distribution comparisons.
   - **Next:** Investigate stock option levels, department-level differences, and potential confounding using multivariable logistic regression.
   - **Further analysis:** Evaluate employee satisfaction, performance ratings, review selection bias, and the robustness of key findings.

2. **Quarto PDF report:** Consolidate Power BI findings and Python statistical results into a reproducible analytical report, including visualizations, methodology, data-quality decisions, interpretation limitations, and actionable HR recommendations.

> **Interpretation note:** The dataset is cross-sectional and does not include employee termination dates. Attrition percentages represent recorded departure proportions, not annual turnover rates. Statistical associations are exploratory and do not establish causality or validate predictions of future employee departures.