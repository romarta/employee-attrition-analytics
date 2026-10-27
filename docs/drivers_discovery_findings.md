# Drivers Discovery — Findings

## Analytical Population

The AI analysis includes 1,217 employees with eligible
performance reviews.

- Employees: 1,217
- Leavers: 224
- Attrition Share: 18.4%

## Key Influencers

Leading associations identified by Power BI:

- OverTime = Yes: 2.96x
- JobRole = Sales Representative: 2.80x
- StockOptionCategory = Level 0: 2.47x
- JobRole = Recruiter: 2.38x
- SalaryBand = Below 45k: 2.31x
- BusinessTravel = Frequent Traveller: 1.78x
- JobRole = Data Scientist: 1.54x
- Department = Sales: 1.52x

These results describe associations, not causal effects.

## AI-Discovered Segments

### Segment 1
- Department != Technology
- OverTime = Yes
- StockOptionCategory = Level 0
- Employees: 62
- Leavers: 38
- Attrition Share: 61.3%

### Segment 2
- Department = Technology
- OverTime = Yes
- StockOptionCategory = Level 0
- Employees: 99
- Leavers: 43
- Attrition Share: 43.4%

### Segment 3
- OverTime = No
- Salary < 45000
- StockOptionCategory = Level 0
- Employees: 96
- Leavers: 30
- Attrition Share: 31.3%

## Interpretation and Limitations

The three segments are mutually exclusive and together
account for approximately 21.1% of the eligible-review
population and 49.6% of recorded leavers in that population.

These segments were discovered and evaluated using
the same dataset. Their observed attrition shares
should not be interpreted as validated predictions.

Deep decomposition-tree paths reached 100% attrition,
but subgroup sizes have not yet been verified.

## Validation

The three identified segments were compared against the full workforce of 1,470 employees.
Together, these segments comprise 314 employees and account for 116 recorded attrition cases.
The segments continued to exhibit elevated attrition rates relative to the overall workforce. However, these findings are based on the same dataset used to identify the segments and therefore do not constitute independent validation.
No independent predictive validation was performed.