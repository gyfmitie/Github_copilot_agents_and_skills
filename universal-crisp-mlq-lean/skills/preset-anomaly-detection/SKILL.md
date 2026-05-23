---
name: preset-anomaly-detection
description: Optional add-on preset for anomaly detection with lean alert-quality checks and false-alarm control.
argument-hint: [entity] [anomaly definition] [alert budget]
---

# Anomaly Detection Preset (Lean)

## Universal default

Use this preset for fast anomaly detection prototypes that still control alert noise.

## Procedure

1. Anomaly definition
- Define anomaly vs normal behavior
- Define monitored entity

2. Evaluation approach
- Labeled, weak-labeled, or unlabeled strategy

3. Minimum baselines
- Rule threshold baseline
- Simple statistical baseline

4. Lean alert validation
- Precision at alert budget
- Duplicate-alert rate
- Time-to-detect snapshot

5. Fallback
- Alert triage owner and suppression rule

## Output format

- Anomaly and scope definition
- Baseline comparison
- Alert-quality summary
- Triage and fallback note

## Project adaptation notes

- Add strict response SLAs for operational teams.
- Add budget caps to avoid alert fatigue.
