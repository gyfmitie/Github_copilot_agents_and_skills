---
name: preset-classification
description: Optional add-on preset for classification projects with threshold policy, class imbalance handling, and error-cost tradeoffs.
argument-hint: [classes] [positive class] [decision threshold]
---

# Classification Preset

## Universal default

Use this preset when outputs are categorical labels or probabilities over classes.

## Procedure

1. Decision framing
- Define class labels and positive class
- Define decision threshold policy
- Define false-positive and false-negative costs

2. Data and label quality
- Check class balance and rare-class coverage
- Validate label noise and ambiguity

3. Baseline set
- Majority-class baseline
- Simple linear/tree baseline

4. Validation pattern
- Stratified split (or time-aware stratification if temporal)
- Per-class precision, recall, and support
- Threshold sweep and operating-point selection

5. Reliability and fallback
- Probability calibration check if probabilities are used
- Fallback rule for low-confidence predictions

## Output format

- Class and threshold policy
- Baseline comparison
- Per-class metrics summary
- Threshold analysis and recommended operating point
- Calibration and fallback summary

## Project adaptation notes

- Add mandated metrics for your domain (for example recall floor for safety tasks).
- Use cost-sensitive evaluation when class errors have asymmetric business impact.
- Add human review for uncertain or high-risk cases.
