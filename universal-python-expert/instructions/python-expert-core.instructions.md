---
name: Python Expert Core Standards
description: Core standards for building production-grade Python tools with architecture-first planning and balanced engineering rigor.
applyTo: "**/*.py"
---

# Python Expert Core Standards

## 1. Environment and Dependency Policy

- Always create and activate an isolated virtual environment before writing or running project code.
- Target Python 3.12+ unless project constraints require otherwise.
- Use `pip` with `requirements.txt` as default dependency workflow.
- Keep dependency manifests synchronized with actual imports.

## 2. Architecture and Code Design

- Prefer modular architecture over monolithic scripts.
- Separate domain logic, IO boundaries, and orchestration layers.
- Keep interfaces explicit and stable.
- Use clear naming and conventional project layout.

## 3. Quality and Reliability

- Use type hints for public interfaces and critical paths.
- Add docstrings for public functions/classes with concise intent and behavior.
- Favor deterministic behavior for data and ML workflows.
- Implement robust input validation and explicit error handling.

## 4. Testing Baseline (Recommended Default)

- Required baseline: unit tests + integration tests for core paths.
- Add property-based tests for transformation-heavy or parser-heavy modules.
- Add at least one smoke end-to-end test per tool entrypoint.
- Keep tests fast, focused, and meaningful to operational behavior.

## 5. Security Baseline

- Run dependency vulnerability checks.
- Run secret scanning.
- Run static security/lint analysis.
- Minimize sensitive data exposure in logs and errors.

## 6. Observability and Operations

- Use structured logging for significant events and failures.
- Define operational metrics and health checks.
- Document fallback and recovery behavior for critical failures.
- Maintain a concise runbook for support and incident response.

## 7. Documentation Requirements

- README with quickstart and setup steps.
- Architecture notes covering major design decisions.
- Contributing guide with quality gates.
- Runbook with operation and troubleshooting guidance.
- Explain formulas and explain how tool outputs should be interpreted.

## 8. Commit Workflow Policy

Before any commit:

1. Provide a brief summary of what changed.
2. Provide a brief summary of why it changed.
3. Ask for explicit acceptance.
4. Then produce concise commit message(s) aligned with scope.

## 9. Assistant Response Behavior

- Default to architecture-first responses with practical implementation detail.
- Provide options with tradeoffs when uncertainty exists.
- State assumptions and unknowns explicitly.
- Prioritize safe, maintainable solutions over novelty.
