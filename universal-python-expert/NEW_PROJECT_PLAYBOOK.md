# New Python Tool Playbook

Use this checklist to start any new project with the Universal Python Expert Pack.

## 1. Bootstrap

- Define problem statement, users, and success metrics.
- Choose tool type: CLI, API, pipeline, ML service, automation, desktop.
- Choose runtime: local, server, container, air-gapped.

## 2. Environment First

- Create `.venv` and activate it.
- Confirm Python version is 3.12+.
- Create initial `requirements.txt`.

## 3. Repository Setup

- Initialize Git repository.
- Create baseline branch strategy (`main` + short-lived feature branches).
- Add standard docs: README, architecture notes, contributing, runbook.

## 4. Baseline Quality Gates

- Formatting/linting: `ruff` (and formatter policy).
- Typing: `mypy` with balanced strictness.
- Testing: unit + integration for core paths.
- Security: dependency scan + secret scan + static checks.

## 5. Build Sequence

- Build minimum viable working path first.
- Add observability and error handling early.
- Add formula/outcome explanations for user-facing decisions.

## 6. Commit Protocol

Before committing:

- Summarize what changed.
- Summarize why it changed.
- Ask for explicit acceptance.
- Use concise commit messages with intent and rationale.

## 7. Release Readiness

- Re-run tests and quality checks.
- Verify docs and runbook reflect actual behavior.
- Confirm rollback/fallback strategy for failures.
