---
name: Energy Domain Guidance
description: Domain-specific guidance for energy and mechanical engineering tools, including physics plausibility, units, and operational value.
applyTo: "**/*.py"
---

# Energy and Mechanical Domain Guidance

## Domain framing

- Tie every proposal to a concrete engineering objective, such as energy reduction, peak demand control, comfort stability, or equipment reliability.
- Define target users and decisions, for example energy manager, plant engineer, or maintenance team.
- Prefer measurable impact statements over generic optimization language.

## Units, signals, and physics

- Always specify units for inputs, outputs, and features.
- Use consistent unit systems and clearly state any conversions.
- Reject physically impossible values and enforce sensible bounds.
- Check first-order plausibility against known engineering relationships before recommending models.

## Data realism

- Evaluate sensor coverage, sampling interval, calibration quality, and outages.
- Consider seasonality, occupancy, weather, and operating schedules.
- Separate commissioning periods, faults, and maintenance windows when possible.
- Explicitly call out data gaps that can bias conclusions.

## Modeling expectations for engineering use

- Favor robust, interpretable approaches for operational adoption unless complexity is clearly justified.
- Compare against rule-based or statistical baselines common in engineering practice.
- Assess performance by operating regime, such as peak load, part load, startup, and shutdown.
- Include uncertainty and confidence communication suitable for operational decisions.

## Value and risk assessment

- Estimate value using low, base, and high scenarios when possible.
- Include implementation effort and maintenance burden in recommendations.
- Identify safety, compliance, and operational risks early.
- Recommend conservative fallback actions when model confidence is low.

## Output style for engineering audiences

- Provide concise recommendations with rationale and assumptions.
- Use clear action-oriented steps, not only model-centric language.
- Distinguish quick wins from longer-term improvements.
- End with a practical validation plan and acceptance criteria.

## Response behavior for the assistant

- Return recommendations in this order:
  - Objective
  - Assumptions
  - Options with tradeoffs
  - Recommended path
  - Validation plan
  - Risks and mitigations
- If key context is missing, ask targeted questions before finalizing.
