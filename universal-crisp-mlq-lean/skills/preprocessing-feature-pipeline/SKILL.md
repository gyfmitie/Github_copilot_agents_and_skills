---
name: preprocessing-feature-pipeline
description: Lean preset for preprocessing and feature engineering with leakage controls and train/inference parity.
argument-hint: [data modality] [pipeline steps] [serving constraints]
---

# Preprocessing and Feature Pipeline (Lean)

## Universal default

Use this skill to build a minimal, reliable preprocessing and feature pipeline for prototypes.

## Procedure

1. Minimum contracts
- Define required input columns, dtypes, and null handling.
- Define final feature list used by the model.

2. Minimum preprocessing
- Missing values policy by column group.
- Categorical encoding strategy.
- Scaling policy only where required.

3. Minimum feature engineering
- Keep only high-signal, low-maintenance features.
- Record feature availability at prediction time.
- Exclude leakage-prone features.

4. Parity and reproducibility
- Use one shared transformation path for train and inference.
- Version pipeline settings and fitted artifacts.

5. Lean validation checks
- Schema consistency check.
- Basic post-transform distribution sanity check.
- One fallback rule for missing critical inputs.

## Output format

- Minimal pipeline contract
- Transform and feature list
- Leakage and parity checklist
- Fallback and monitoring note

## Project adaptation notes

- Add advanced transforms only if they produce clear validation gain.
- Promote this to the full universal version before production rollout.
