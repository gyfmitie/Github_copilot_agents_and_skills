---
name: CRISP-ML(Q) Core Universal Policy
description: Universal lifecycle guardrails for ML projects following CRISP-ML(Q), with phase gates, quality criteria, and adaptation notes.
applyTo: "**/*.{py,ipynb,sql,yml,yaml,md}"
---

# CRISP-ML(Q) Core Universal Policy

## Universal default

Use CRISP-ML(Q) as an end-to-end lifecycle:

1. Business and data understanding
2. Data preparation
3. Modeling
4. Evaluation and quality assurance
5. Deployment
6. Monitoring and maintenance

Treat quality as continuous, not a final step.

## Required outputs per phase

1. Problem framing artifact
- Decision objective
- Target variable
- Success and failure impact
- Constraints (latency, cost, explainability, regulation)

2. Data readiness artifact
- Data sources and ownership
- Data quality checks
- Leakage boundary definition
- Label quality and timestamp integrity

3. Modeling artifact
- Baseline model
- Candidate model(s)
- Feature rationale
- Reproducibility settings (seed, versions, config)

4. Validation artifact
- Split strategy aligned to deployment
- Regime or segment-level metrics
- Error decomposition
- Uncertainty quality (if applicable)

5. Deployment artifact
- Interface contract and dependencies
- Rollout plan and fallback
- Monitoring KPIs and alerts

6. Maintenance artifact
- Drift detection policy
- Retraining triggers
- Ownership and incident response

## Non-negotiable quality gates

- No deployment recommendation without baseline comparison.
- No leakage-prone feature allowed without explicit mitigation.
- No global metric-only reporting: include segment or regime diagnostics.
- No uncertainty claims without calibration evidence when uncertainty is used.
- No productionization without fallback behavior for low-confidence or failed predictions.

## Version control and change management

- Use version control from project start, with repository initialization if missing.
- Require branch-based development for model, data pipeline, and evaluation changes.
- Keep commits small, reviewable, and linked to phase artifacts or decisions.
- Preserve reproducibility evidence in history (for example config updates, data/version notes, metric reports).
- Prefer reviewed merges for major lifecycle transitions (for example baseline acceptance, deployment recommendation).

## Response behavior for assistant

When asked to propose or review ML work:

1. Identify CRISP-ML(Q) phase(s) involved.
2. State assumptions and unknowns explicitly.
3. Provide at least two options with tradeoffs.
4. Recommend one option tied to decision impact.
5. List missing artifacts required to pass quality gates.
6. Use plain language and include one small concrete example when introducing a method or quality gate.
7. If version control setup is missing, include repository setup, branch strategy, and merge checkpoints as explicit actions.

## Project adaptation notes

Adjust this file per project by editing these sections:

- `applyTo`
  - Add `ipynb` for notebook-heavy projects.
  - Narrow to specific folders for large monorepos.

- `Required outputs per phase`
  - Add domain-specific artifacts:
    - Medical: clinical safety case
    - Finance: model risk documentation
    - Industrial controls: safety interlock validation

- `Non-negotiable quality gates`
  - Remove gates only if your governance explicitly permits it.
  - Add legal/compliance constraints for regulated domains.

- `Response behavior`
  - Tighten verbosity, formatting, and preferred decision templates.
