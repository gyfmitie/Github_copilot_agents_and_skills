---
name: Python ML Engineering Standards
description: Standards for Python machine learning development with reproducibility, maintainability, and reliable evaluation.
applyTo: "**/*.py"
---

# Python ML Engineering Standards

## Code quality

- Prefer clear, modular functions over long scripts.
- Use type hints for function inputs and outputs.
- Write concise docstrings for public functions and classes.
- Avoid hidden side effects inside utility functions.
- Use structured logging for important pipeline steps instead of ad hoc prints.

## Reproducibility

- Set and document random seeds for data splitting, model training, and sampling.
- Make configuration explicit through constants or config objects.
- Record key experiment metadata: data version, feature set, model version, and hyperparameters.
- Keep training and inference preprocessing consistent and reusable.

## Environment bootstrap and dependency isolation

- Create and activate an isolated Python environment before running project code.
- Prefer a project-local environment (for example `.venv`) to reduce cross-project conflicts.
- Pin and document the Python version used by the project.
- Capture dependencies in a reproducible manifest (for example `requirements.txt` or `pyproject.toml`).
- Update dependency manifests when packages change, and keep setup steps in project documentation.

## Version control and change management

- Initialize Git at project start if not already initialized.
- Use short-lived feature branches for changes instead of committing directly to the main branch.
- Make small, focused commits with clear intent and traceable rationale.
- Keep commit messages consistent (for example imperative style with scope when useful).
- Merge through reviewed pull requests where possible, and preserve a readable history.
- Tag or release-marker key milestones (for example first validated baseline, production candidate).

## Data and feature handling

- Validate schema early: required columns, dtypes, and missing critical fields.
- Handle missing values explicitly and document the chosen strategy.
- Prevent target leakage by separating future information from training features.
- Prefer explainable baseline features first, then add complex engineered features.

## Modeling workflow

- Start with a baseline model before advanced models.
- Choose model complexity based on data volume, noise, and operational constraints.
- Use time-aware validation for time-dependent data.
- Report performance with task-relevant metrics and baseline comparison.

## Evaluation and reliability

- Include error analysis by segment or operating regime, not only global averages.
- Report uncertainty where meaningful, such as prediction intervals or confidence bands.
- Highlight model limits and known failure modes.
- Define fallback behavior for low-confidence predictions.

## Engineering and deployment

- Keep pipeline steps deterministic where possible.
- Design for maintainability by engineers who are not ML specialists.
- Expose important thresholds and parameters in configuration, not hard-coded values.
- Add lightweight tests for data validation and core pipeline logic.

## Response behavior for the assistant

- When proposing solutions, provide at least two options with tradeoffs.
- State assumptions and unknowns explicitly.
- Prefer practical implementation plans with phased milestones.
- If critical information is missing, ask focused clarification questions before final recommendations.
- If environment setup is missing, include environment bootstrap and dependency capture as explicit first steps.
- If version control setup is missing, include repository initialization, branch strategy, and commit plan as explicit first steps.
