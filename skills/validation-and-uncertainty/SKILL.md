---
name: validation-and-uncertainty
description: Design robust validation plans for engineering ML tools with time-aware splits, regime-level error analysis, and uncertainty reporting.
argument-hint: [model type] [target] [operating regimes]
---

# Validation and Uncertainty

Use this skill when evaluating model performance claims.

## Procedure

1. Validation design
- Time-based splits
- Backtesting windows
- Regime-aware holdouts

2. Metric strategy
- Primary metric tied to decision impact
- Secondary metrics for robustness
- Cost-weighted error metric when possible

3. Regime-level diagnostics
- Peak-load periods
- Startup/shutdown behavior
- Seasonal and occupancy shifts

4. Uncertainty
- Prediction intervals
- Confidence calibration checks
- Escalation rules for low confidence

5. Reliability and drift
- Production monitoring metrics
- Drift thresholds and retraining triggers
- Fallback mode definition

## Output format

- Validation verdict: Pass, Conditional pass, Fail
- Performance summary by regime
- Uncertainty quality summary
- Deployment guardrails
- Retraining policy recommendation