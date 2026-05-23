---
name: preprocessing-feature-pipeline
description: Design and validate preprocessing and feature engineering pipelines with train/inference parity, leakage controls, and reproducibility.
argument-hint: [data modality] [pipeline steps] [serving constraints]
---

# Preprocessing and Feature Pipeline

## Universal default

Use this skill when defining or reviewing data preprocessing and feature engineering before modeling and deployment.

## Procedure

1. Pipeline scope and contracts
- Define input schema, expected dtypes, units, and null policy.
- Define output feature schema with names, types, and semantic meaning.
- Document which transforms run at training only, inference only, or both.

2. Core preprocessing design
- Missing values: strategy per feature group (drop, impute, flag).
- Outliers: clip, winsorize, robust transform, or pass-through with rationale.
- Encoding: categorical strategy (one-hot, target, ordinal with ordering rules).
- Scaling/normalization: define where required and where forbidden.

3. Feature engineering design
- Derive candidate features from domain logic and operational availability.
- Tag each feature with source, latency, and prediction-time availability.
- Remove or quarantine leakage-prone and post-outcome features.

4. Train/inference parity and reproducibility
- Reuse the same transformation logic and parameters across train and serve paths.
- Version preprocessing pipeline and feature definitions.
- Freeze fitted artifacts (encoders, imputers, scalers) with clear version IDs.

5. Validation checks
- Schema drift checks between train, validation, and serving samples.
- Distribution checks for critical features after transforms.
- Pipeline unit checks (for example no negative values after constrained transforms).

6. Operational safeguards
- Fallback behavior for missing critical inputs at inference.
- Monitoring signals for transform failures and feature null spikes.
- Rollback plan for bad feature releases.

## Output format

- Pipeline contract summary
- Preprocessing decision table
- Feature catalog (source, transform, availability, leakage risk)
- Parity and reproducibility checklist
- Validation and monitoring checklist

## Project adaptation notes

- Add modality-specific steps:
  - Time series: lag windows, alignment rules, and leakage guards.
  - Tabular: categorical cardinality controls and rare-category policy.
  - Text: tokenization/version pinning and OOV handling.
  - Images: augmentation boundaries and deterministic inference transforms.
- Remove transforms that are unnecessary for tree-based models where appropriate.
- Add feature store references if your team uses one.
- Add strict approval gates for high-impact regulated use cases.
