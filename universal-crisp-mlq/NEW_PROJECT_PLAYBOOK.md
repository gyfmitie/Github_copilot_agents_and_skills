# New Project Playbook (Beginner-Friendly)

This guide shows exactly how to start a new ML project using your CRISP-ML(Q) pack.

## Big picture

- Instruction = always-on rules for your project
- Skills = practical checklists for specific tasks
- Agents = planning and review helpers

## Step 0: Bootstrap your Python environment

Create and activate a dedicated virtual environment before you write or run project code.

Suggested commands:

- Windows (PowerShell)
	- `python -m venv .venv`
	- `.\.venv\Scripts\Activate.ps1`
- macOS/Linux
	- `python3 -m venv .venv`
	- `source .venv/bin/activate`

Then initialize dependencies and lock them:

- `python -m pip install --upgrade pip`
- Install your initial packages
- `pip freeze > requirements.txt`

Document the Python version and setup steps in your project README so others can reproduce the environment.

Initialize version control before starting feature work:

- `git init`
- `git checkout -b chore/project-bootstrap`
- Make an initial commit for environment and project scaffolding

Use feature branches for each meaningful change and merge back after review.

## Step 1: Copy a pack into your new project

1. Create a `.Copilot` folder in your new project.
2. Copy one full pack:
- Full pack: `universal-crisp-mlq`
- Fast prototype pack: `universal-crisp-mlq-lean`

## Step 2: Set instruction scope (`applyTo`)

Open:
- `instructions/crisp-mlq-core.instructions.md`

Pick one:
- Python only: `"**/*.py"`
- Python + notebooks: `"**/*.{py,ipynb}"`
- Mixed ML repo: `"**/*.{py,ipynb,sql,yml,yaml,md}"`

## Step 3: Pick one project-type preset

Choose one primary preset based on your task:
- Forecasting: `skills/preset-forecasting/SKILL.md`
- Classification: `skills/preset-classification/SKILL.md`
- Anomaly detection: `skills/preset-anomaly-detection/SKILL.md`

## Step 4: Use core skills alongside the preset (exact example)

You always use a preset together with core skills, not alone.

### Example scenario

Project goal: predict next-day building energy use (forecasting)

Primary preset:
- `skills/preset-forecasting/SKILL.md`

Core skills used with it:
- `skills/data-readiness/SKILL.md`
- `skills/preprocessing-feature-pipeline/SKILL.md`
- `skills/modeling-baseline/SKILL.md`
- `skills/validation-uncertainty/SKILL.md`

### How to run this in practice

1. Use `data-readiness`
- Check missing timestamps, schema issues, duplicates, and leakage boundary.
- Output: readiness verdict and data issues list.

2. Use `preprocessing-feature-pipeline`
- Define exact transforms: imputation, encoding, scaling, feature availability timing.
- Output: transform contract and feature catalog.

3. Use `preset-forecasting`
- Define horizon and cadence, select seasonal naive baseline, set rolling validation.
- Output: forecasting spec + baseline table + walk-forward backtest setup.

4. Use `modeling-baseline`
- Train simple baseline and one candidate model with reproducible settings.
- Output: baseline comparison and model selection criteria.

5. Use `validation-uncertainty`
- Evaluate by regime (weekday/weekend, season) and confidence quality.
- Output: pass/conditional/fail with follow-up actions.

### Example prompts you can paste

- "Use data-readiness to audit my dataset before feature engineering."
- "Use preprocessing-feature-pipeline to define my train/inference transforms and leakage-safe feature list."
- "Use preset-forecasting to set horizon, baseline, and rolling backtest windows."
- "Use modeling-baseline to compare seasonal naive vs my first model."
- "Use validation-uncertainty to report regime-level errors and confidence quality."

## Step 5: Use the Architect agent for planning

Use:
- `agents/crisp-mlq-architect.agent.md`

Example prompt:
- "Use CRISP-ML(Q) architect to create a 2-week plan for this forecasting project with milestones and acceptance checks."

## Step 6: Build your first baseline

Keep it simple first:
- Load data
- Apply preprocessing pipeline
- Train baseline
- Evaluate with primary metric
- Save results and assumptions

## Step 7: Use the Auditor agent before trusting results

Use:
- `agents/crisp-mlq-auditor.agent.md`

Example prompt:
- "Audit my baseline setup against CRISP-ML(Q) gates and list missing items before production."

## Step 8: Iterate with a simple loop

1. Architect plans
2. You implement
3. Auditor reviews
4. You fix gaps
5. Repeat

## Quick checklist for each new project

- Virtual environment created and activated
- Python version documented
- Dependency manifest created and updated
- Git repository initialized
- Branch strategy defined (feature branches plus merge flow)
- Initial bootstrap commit created
- One primary preset selected
- Core skills used with preset
- Baseline comparison completed
- Leakage checks documented
- Regime-level validation completed
- Clear fallback behavior defined

## Git workflow quick prompts

- "Create a branch named feat/<topic>, make the requested changes, and commit them in small logical commits. Do not push."
- "Prepare a safe merge plan for branch feat/<topic> into main and stop before merging."
- "Merge branch feat/<topic> into main with a merge commit, resolve conflicts conservatively, and summarize the result."
- "Rebase branch feat/<topic> onto main, then fast-forward merge if possible. Stop and ask if conflicts appear."
- "Show the current branch, recent commits, and the cleanest next Git step for this work."
