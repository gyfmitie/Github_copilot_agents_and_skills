# Universal Python Expert Pack

A reusable agent/skills toolkit for building production-grade Python tools across:

- CLI applications
- FastAPI services
- Data and ETL pipelines
- ML training and inference workflows
- Automation tools
- Desktop applications

## Design Defaults

- Python 3.12+
- `pip` + `requirements.txt`
- Virtual environment first, always
- Balanced engineering strictness
- Architecture-first reasoning with implementation-ready output
- Security by default (dependency scan, secret scan, static security lint)

## Structure

- `agents/` expert implementation and audit agents
- `instructions/` cross-cutting coding standards and workflow rules
- `skills/` focused capabilities for common engineering tasks

## Included Agents

- `python-tooling-architect`: implementation planner and builder
- `python-tooling-auditor`: risk, quality, and readiness reviewer

## Included Skills

- project-bootstrap
- api-service-design
- data-pipeline-reliability
- ml-service-patterns
- testing-strategy
- observability-ops
- security-compliance
- performance-profiling
- packaging-release
- desktop-app-foundations
- documentation-explainability
- refactoring-hardening

## Operating Rules Encoded

1. Create and activate an isolated virtual environment before coding.
2. Use clear project layout and standard naming.
3. Before any commit, summarize what changed and why, then ask for acceptance.
4. Prefer deterministic, testable, maintainable implementations over clever shortcuts.
