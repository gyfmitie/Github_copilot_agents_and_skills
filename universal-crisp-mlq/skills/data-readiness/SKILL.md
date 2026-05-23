---
name: data-readiness
description: Assess whether data quality, labeling, and temporal integrity are sufficient for ML.
argument-hint: [data sources] [label process] [time granularity]
---

# Data Readiness

## Universal default

Use this skill before feature engineering and model training.

## Procedure

1. Source and ownership audit
- Identify source systems and refresh cadence.
- Identify data owners and operational dependencies.

2. Schema and quality checks
- Required fields, dtypes, ranges, missingness, duplicates.
- Timestamp continuity and timezone consistency.

3. Leakage and causality boundary
- Verify features available at prediction time.
- Remove post-outcome and proxy-leakage features.

4. Label quality assessment
- Label generation process and delay.
- Ambiguity and annotation consistency.

5. Coverage analysis
- Regime, segment, and seasonal coverage.

## Output format

- Data inventory
- Quality findings
- Leakage risk assessment
- Label reliability summary
- Readiness verdict (Ready, Conditional, Not ready)

## Project adaptation notes

- Add domain-specific quality checks (for example sensor plausibility).
- Remove checks that do not apply to static tabular datasets.
- Add data retention and privacy constraints if required.
