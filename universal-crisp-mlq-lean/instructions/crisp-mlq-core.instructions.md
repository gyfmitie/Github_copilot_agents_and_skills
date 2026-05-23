---
name: CRISP-ML(Q) Core Lean Policy
description: Lean lifecycle guardrails for fast ML prototyping with CRISP-ML(Q), keeping essential quality checks.
applyTo: "**/*.{py,ipynb,sql,yml,yaml,md}"
---

# CRISP-ML(Q) Core Lean Policy

## Universal default

Use CRISP-ML(Q) as an end-to-end lifecycle:

1. Business and data understanding
2. Data preparation
3. Modeling
4. Evaluation and quality assurance
5. Deployment
6. Monitoring and maintenance

Treat quality as continuous, not a final step.

This lean variant prioritizes speed to a trustworthy baseline before full production governance.

## Required outputs per phase (lean minimum)

1. Problem framing artifact
- Decision objective
- Target variable
- Success impact and critical failure risk

2. Data readiness artifact
- Data sources and ownership
- Data quality checks
- Leakage boundary definition
- Label quality notes

3. Modeling artifact
- Baseline model
- Feature rationale
- Reproducibility settings (seed, versions, config)

4. Validation artifact
- Split strategy aligned to deployment
- One primary metric and key segment checks
- Optional uncertainty quality summary if uncertainty is used

5. Deployment artifact
- Optional for prototype stage; required before production
- Define at minimum a fallback decision path

6. Maintenance artifact
- Optional for prototype stage; required before production

## Environment bootstrap and dependency isolation

- Create and activate an isolated Python environment before running project code.
- Prefer a project-local environment (for example `.venv`) to reduce cross-project conflicts.
- Pin and document the Python version used by the project.
- Capture dependencies in a reproducible manifest (for example `requirements.txt` or `pyproject.toml`).
- Update dependency manifests when packages change, and keep setup steps in project documentation.

## Version control and change management

- Use version control from project start, with repository initialization if missing.
- Use short-lived feature branches for experiment, pipeline, and evaluation updates.
- Keep commits small and reviewable, tied to specific prototype decisions.
- Preserve baseline evidence in history (for example config, data notes, and metric snapshots).
- Use clear merge points between prototype milestones to keep iteration history understandable.

## Non-negotiable quality gates

- No deployment recommendation without baseline comparison.
- No leakage-prone feature allowed without explicit mitigation.
- No global metric-only reporting: include at least one segment or regime diagnostic.
- No uncertainty claims without simple calibration evidence when uncertainty is used.
- No productionization without fallback behavior for low-confidence or failed predictions.

## Response behavior for assistant

When asked to propose or review ML work:

1. Identify CRISP-ML(Q) phase(s) involved.
2. State assumptions and unknowns explicitly.
3. Provide one recommended path and one backup option with tradeoffs.
4. List missing artifacts required for the current stage.
5. Use plain language and include one small concrete example when introducing a method or quality gate.
6. If environment setup is missing, include environment bootstrap and dependency capture as explicit first steps.
7. If version control setup is missing, include repository setup, branch strategy, and merge checkpoints as explicit first steps.

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
  - Promote optional prototype artifacts to required when moving to production.

- `Non-negotiable quality gates`
  - Remove gates only if your governance explicitly permits it.
  - Add legal/compliance constraints for regulated domains.

- `Response behavior`
  - Tighten verbosity, formatting, and preferred decision templates.
