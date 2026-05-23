---
name: modeling-baseline
description: Establish baseline and candidate model strategy with reproducible training setup.
argument-hint: [task type] [baseline] [candidate models]
---

# Modeling and Baseline

## Universal default

Use this skill when selecting model class and training workflow.

## Procedure

1. Baseline first
- Define simple baseline and expected performance floor.
- Explain why baseline is operationally meaningful.

2. Candidate model strategy
- Select models based on data volume, noise, and constraints.
- Define hyperparameter search scope.

3. Reproducibility controls
- Random seeds, package versions, and deterministic settings.
- Config-driven parameters instead of hard-coded constants.

4. Feature governance
- Feature rationale and removals.
- Explainability requirements for chosen model class.

## Output format

- Baseline design and metric
- Candidate model shortlist
- Training protocol
- Reproducibility checklist
- Model selection criteria

## Project adaptation notes

- Add mandatory model classes if your organization has standards.
- Remove advanced search if budget or timeline is limited.
- Add explainability policy for regulated or high-impact use cases.
