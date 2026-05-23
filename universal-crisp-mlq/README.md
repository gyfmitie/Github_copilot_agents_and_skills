# Universal CRISP-ML(Q) Copilot Pack

This folder is a reusable starter pack for applying CRISP-ML(Q) across different Python ML projects.

## What is included

- `instructions/crisp-mlq-core.instructions.md`
  - Always-on project-level policy and quality gates.
- `agents/crisp-mlq-architect.agent.md`
  - Designs implementation options and plans per CRISP-ML(Q) phase.
- `agents/crisp-mlq-auditor.agent.md`
  - Reviews artifacts and decisions against quality criteria.
- `skills/problem-framing/SKILL.md`
- `skills/data-readiness/SKILL.md`
- `skills/preprocessing-feature-pipeline/SKILL.md`
- `skills/modeling-baseline/SKILL.md`
- `skills/validation-uncertainty/SKILL.md`
- `skills/deployment-monitoring/SKILL.md`
- `skills/fairness-risk-governance/SKILL.md`

Optional project-type add-on presets:

- `skills/preset-forecasting/SKILL.md`
- `skills/preset-classification/SKILL.md`
- `skills/preset-anomaly-detection/SKILL.md`

## Universal-by-default design

Each file contains sections labeled:

- `Universal default`
- `Project adaptation notes`

Use these notes to decide what to keep, edit, or remove for each project.

Default profile in this draft:

- Scope: Python scripts, notebooks, and common ML support files
- Governance: balanced (strict core quality gates, fairness/governance as context-dependent)
- Agent style: plain language, medium structure, with short practical examples

## How to use in a new project

1. Copy this entire folder into your project under `.Copilot/`.
2. Start by editing:
   - `instructions/crisp-mlq-core.instructions.md`
3. Update `applyTo` patterns for your stack:
   - Python only: `"**/*.py"`
   - Notebooks: `"**/*.{py,ipynb}"`
   - Polyglot projects: broaden patterns as needed.
4. Remove skills that do not apply:
   - Example: remove fairness skill for purely internal, non-human-impact optimization if your governance permits that.
5. Add project-specific skills when needed:
   - Example: geospatial QA, sensor fault diagnostics, LLM eval.
6. Activate one optional project-type preset when applicable:
   - Forecasting projects: `preset-forecasting`
   - Classification projects: `preset-classification`
   - Anomaly detection projects: `preset-anomaly-detection`
7. Add `preprocessing-feature-pipeline` when you need explicit transform contracts, parity checks, and feature cataloging.

## Suggested minimum adaptation checklist

- Problem statement, target variable, and decision impact are explicit.
- Data contracts and leakage boundaries are defined.
- Baseline model and acceptance threshold are defined.
- Time-aware and regime-aware validation are defined.
- Uncertainty output and low-confidence fallback are defined.
- Deployment monitoring and retraining triggers are defined.
- Compliance or governance constraints are documented.

## Optional cleanup for narrow projects

You can simplify by removing:

- Agent files if you only use direct chat + instructions/skills.
- Fairness/governance skill if project scope and policy truly do not require it.
- Deployment skill for one-off exploratory analysis.

Keep at least the core instruction and validation skill for quality control.
