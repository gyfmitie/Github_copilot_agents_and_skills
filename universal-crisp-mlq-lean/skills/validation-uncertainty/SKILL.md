---
name: validation-uncertainty
description: Design robust validation with split logic, regime diagnostics, and uncertainty quality checks.
argument-hint: [split strategy] [primary metric] [regimes]
---

# Validation and Uncertainty

## Universal default

Use this skill before claiming readiness for deployment.
For lean prototyping, run a minimal but defensible validation set.

## Procedure

1. Validation design
- Use split strategy that mirrors deployment timing.
- Include backtesting or rolling windows for time-dependent tasks.

2. Metric strategy
- Primary metric tied to decision impact.
- One or two secondary metrics for robustness and calibration.

3. Regime diagnostics
- Segment by operating regimes, cohorts, or context bands.
- Report worst-case segment performance.

4. Uncertainty quality
- Define interval or confidence method.
- Check calibration and empirical coverage when uncertainty output is used.

5. Acceptance criteria
- Define pass/fail thresholds and escalation rules.

## Output format

- Validation plan
- Metrics and thresholds
- Regime-level findings
- Uncertainty quality summary
- Verdict (Pass, Conditional pass, Fail)

## Project adaptation notes

- Add regulated-domain validation constraints where required.
- Remove uncertainty section only if outputs are strictly deterministic and policy allows it.
- Add custom cost-weighted metrics if business cost is asymmetric.
