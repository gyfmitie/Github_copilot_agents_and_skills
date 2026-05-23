# Beginner Playbook for This Repository

This guide helps beginners understand what each folder/file does and where to start.

## 1) What this repository contains

You have three layers of reusable Copilot assets:

- Domain-specific assets for building energy workflows at the repository root.
- A full CRISP-ML(Q) starter pack in universal-crisp-mlq.
- A lean CRISP-ML(Q) starter pack in universal-crisp-mlq-lean.

## 2) Fast start (first 15 minutes)

1. Read README.md at the repository root.
2. Decide your path:
- Building energy project: use root agents/instructions/skills first.
- General ML project with fuller governance: use universal-crisp-mlq.
- Fast prototype: use universal-crisp-mlq-lean.
3. Keep one pack as your primary base to avoid conflicting guidance.
4. Add only the skills you need for your current task.

## 3) Complete file map (what each file is for)

### Root files

- LICENSE: repository license terms.
- README.md: top-level overview of all packs and intended usage.

### Root domain agents

- agents/energy-assessor.agent.md: specialized agent persona for building energy assessment workflows.

### Root domain instructions

- instructions/building-energy-features.instructions.md: guidance for energy-focused feature engineering.
- instructions/building-energy-forecasting.instructions.md: guidance for energy forecasting setups and checks.
- instructions/energy-domain.instructions.md: domain context and constraints for energy tasks.
- instructions/python-ml.instructions.md: general Python ML coding and workflow guidance.

### Root domain skills

- skills/data-quality-audit/SKILL.md: checks for schema quality, missingness, anomalies, and readiness.
- skills/feasibility-screening/SKILL.md: early go/no-go checks before expensive modeling.
- skills/validation-and-uncertainty/SKILL.md: validation depth, uncertainty handling, and reliability checks.

### Full pack: universal-crisp-mlq

Core docs:
- universal-crisp-mlq/README.md: what the full pack includes and how to adapt it.
- universal-crisp-mlq/NEW_PROJECT_PLAYBOOK.md: step-by-step starter process for a new project.

Agents:
- universal-crisp-mlq/agents/crisp-mlq-architect.agent.md: planning/design agent across CRISP-ML(Q) phases.
- universal-crisp-mlq/agents/crisp-mlq-auditor.agent.md: audit/review agent for quality gates and risk checks.

Instruction:
- universal-crisp-mlq/instructions/crisp-mlq-core.instructions.md: always-on core policy and quality framework.

Core skills:
- universal-crisp-mlq/skills/problem-framing/SKILL.md: define problem, decision impact, and success criteria.
- universal-crisp-mlq/skills/data-readiness/SKILL.md: assess data contracts, provenance, and leakage boundaries.
- universal-crisp-mlq/skills/preprocessing-feature-pipeline/SKILL.md: define transformations and train/inference parity.
- universal-crisp-mlq/skills/modeling-baseline/SKILL.md: establish baseline and candidate model comparisons.
- universal-crisp-mlq/skills/validation-uncertainty/SKILL.md: robust validation and confidence/uncertainty reporting.
- universal-crisp-mlq/skills/deployment-monitoring/SKILL.md: monitoring, drift checks, and retraining triggers.
- universal-crisp-mlq/skills/fairness-risk-governance/SKILL.md: fairness, policy, and governance controls.

Optional presets:
- universal-crisp-mlq/skills/preset-forecasting/SKILL.md: forecasting-specific defaults.
- universal-crisp-mlq/skills/preset-classification/SKILL.md: classification-specific defaults.
- universal-crisp-mlq/skills/preset-anomaly-detection/SKILL.md: anomaly detection-specific defaults.

### Lean pack: universal-crisp-mlq-lean

Core docs:
- universal-crisp-mlq-lean/README.md: lightweight pack overview and usage.

Agents:
- universal-crisp-mlq-lean/agents/crisp-mlq-architect.agent.md: lean planning/design agent.
- universal-crisp-mlq-lean/agents/crisp-mlq-auditor.agent.md: lean review/audit agent.

Instruction:
- universal-crisp-mlq-lean/instructions/crisp-mlq-core.instructions.md: lean always-on policy and checks.

Skills:
- universal-crisp-mlq-lean/skills/problem-framing/SKILL.md
- universal-crisp-mlq-lean/skills/data-readiness/SKILL.md
- universal-crisp-mlq-lean/skills/preprocessing-feature-pipeline/SKILL.md
- universal-crisp-mlq-lean/skills/modeling-baseline/SKILL.md
- universal-crisp-mlq-lean/skills/validation-uncertainty/SKILL.md
- universal-crisp-mlq-lean/skills/deployment-monitoring/SKILL.md
- universal-crisp-mlq-lean/skills/fairness-risk-governance/SKILL.md
- universal-crisp-mlq-lean/skills/preset-forecasting/SKILL.md
- universal-crisp-mlq-lean/skills/preset-classification/SKILL.md
- universal-crisp-mlq-lean/skills/preset-anomaly-detection/SKILL.md

## 4) Which path should a beginner choose?

Choose one:

- Path A (energy-focused): start at root instructions + root skills + energy-assessor agent.
- Path B (full governance): start with universal-crisp-mlq/NEW_PROJECT_PLAYBOOK.md, then architect and auditor agents.
- Path C (faster adoption): start with universal-crisp-mlq-lean and add only required skills.

## 5) Suggested first-week routine

1. Day 1: Problem framing + data readiness.
2. Day 2: Preprocessing and feature pipeline definition.
3. Day 3: Baseline model and metrics.
4. Day 4: Validation and uncertainty checks.
5. Day 5: Auditor pass and action list.

## 6) Common beginner mistakes to avoid

- Mixing full and lean packs in the same active workflow.
- Skipping baseline creation before complex models.
- Ignoring leakage boundaries during feature design.
- Treating presets as replacement for core skills.
- Moving to deployment checks before validation is stable.

## 7) If you want one single starting point

Use this order:

1. README.md (root)
2. universal-crisp-mlq/NEW_PROJECT_PLAYBOOK.md
3. universal-crisp-mlq/instructions/crisp-mlq-core.instructions.md
4. universal-crisp-mlq/skills/problem-framing/SKILL.md
5. universal-crisp-mlq/skills/data-readiness/SKILL.md

After that, proceed skill-by-skill based on your project type.
