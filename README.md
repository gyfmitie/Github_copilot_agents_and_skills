# GitHub Copilot Agents and Skills

This repository is a curated toolkit of custom GitHub Copilot assets for practical machine learning workflows.

It includes:
- Custom agents for specialized guidance and review
- Instruction files for domain and workflow constraints
- Reusable skills for repeatable ML tasks
- Two CRISP-ML(Q) starter packs (full and lean)

The goal is to make project setup, modeling, validation, and governance more consistent and easier to scale across use cases.

## What You Will Find

### Top-level assets
- `agents/`: Custom agent definitions (for example, energy assessment workflows)
- `instructions/`: Reusable instruction sets (domain, forecasting, Python/ML guidance)
- `skills/`: Focused skills such as data-quality auditing, feasibility screening, and uncertainty checks

### CRISP-ML(Q) templates
- `universal-crisp-mlq/`: Full template with playbook, architect/auditor agents, and end-to-end skills
- `universal-crisp-mlq-lean/`: Lightweight version of the same pattern for faster adoption

## Repository Purpose

Use this repository as a reference and starting point to:
1. Standardize AI-assisted ML project workflows
2. Reuse high-quality prompts and process guidance
3. Improve consistency across data readiness, modeling, deployment, and risk controls
4. Accelerate onboarding for new projects and contributors

## Typical Usage

1. Pick a template:
	- Use `universal-crisp-mlq/` for full governance and delivery flow
	- Use `universal-crisp-mlq-lean/` for a lighter setup
2. Select relevant instructions and skills for your use case
3. Adapt agents/instructions to your domain language and constraints
4. Run your project using the adapted assets as your Copilot guidance layer

## Who This Is For

- ML practitioners who want a structured project workflow
- Teams using GitHub Copilot for repeatable engineering and data science tasks
- Anyone building domain-specific prompt assets for quality and governance

## Notes

- This repository focuses on process assets (agents, instructions, skills), not model binaries or datasets.
- You can copy and adapt individual components independently.

## License

This repository is licensed under Creative Commons Attribution 4.0 International (CC BY 4.0).

See [LICENSE](LICENSE) for the full text.
