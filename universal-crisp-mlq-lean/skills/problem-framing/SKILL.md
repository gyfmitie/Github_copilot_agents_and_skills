---
name: problem-framing
description: Define business objective, prediction target, and decision impact before modeling.
argument-hint: [use case] [target] [decision]
---

# Problem Framing

## Universal default

Use this skill when the objective, target, or decision impact is unclear.
For lean prototyping, keep this to a short one-page decision brief.

## Procedure

1. Objective definition
- State what decision this model supports.
- Define success criteria and acceptable failure modes.

2. Target specification
- Define target variable, unit, and prediction horizon.
- Define when ground truth is available.

3. Scope and constraints
- Latency, cost, interpretability, privacy, compliance.

4. Baseline decision policy
- Define no-model baseline process.
- Define minimum improvement needed to justify ML.

## Output format

- Problem statement
- Target and labels
- Decision impact summary
- Top constraints only
- Baseline policy
- Go or no-go criteria

## Project adaptation notes

- Add domain constraints (for example medical safety thresholds).
- Remove irrelevant constraints for internal prototypes.
- Add specific stakeholders and sign-off owners.
