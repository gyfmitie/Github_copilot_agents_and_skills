---
name: data-quality-audit
description: Audit engineering and energy datasets for missingness, consistency, drift, unit integrity, and suitability for ML.
argument-hint: [dataset description] [target variable] [time range]
---

# Data Quality Audit

Use this skill before model training or model updates.

## Audit checks

1. Schema integrity
- Required fields present
- Types and units consistent

2. Time integrity
- Timestamp continuity
- Duplicate and out-of-order records
- Timezone consistency

3. Missingness and outliers
- Missing data by feature and by period
- Extreme values and sensor spikes

4. Target integrity
- Label delays, leakage candidates
- Distribution shifts across seasons/regimes

5. Engineering sanity checks
- Physical bounds and impossible values
- Cross-sensor consistency rules

## Output format

- Data quality score: 0 to 100
- Critical issues
- Warning issues
- Leakage risk assessment
- Recommended cleaning and feature actions
- Data acceptance verdict: Train-ready, Conditionally ready, Not ready