---
name: preset-classification
description: Optional add-on preset for classification projects with lean threshold and class-imbalance checks.
argument-hint: [classes] [positive class] [threshold]
---

# Classification Preset (Lean)

## Universal default

Use this preset for fast classification prototypes with clear decision thresholds.

## Procedure

1. Target and threshold
- Define classes and positive class
- Define initial decision threshold

2. Data checks
- Class balance
- Rare-class coverage

3. Minimum baselines
- Majority-class baseline
- Simple linear/tree baseline

4. Lean validation
- Stratified split (time-aware if temporal)
- Precision/recall/F1 at chosen threshold
- Quick threshold sweep

5. Fallback
- Define action for low-confidence cases

## Output format

- Class policy
- Baseline comparison
- Threshold summary
- Fallback note

## Project adaptation notes

- Add mandated domain metrics when needed.
- Add human review for uncertain high-impact cases.
