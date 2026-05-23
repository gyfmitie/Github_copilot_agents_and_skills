---
name: preset-anomaly-detection
description: Optional add-on preset for anomaly detection projects with event definition, alert quality, and false-alarm control.
argument-hint: [entity] [anomaly definition] [alert budget]
---

# Anomaly Detection Preset

## Universal default

Use this preset when the goal is to detect rare abnormal behavior or events.

## Procedure

1. Event definition
- Define what counts as anomaly vs. normal variation
- Define entity scope (asset, user, transaction, meter)

2. Label strategy
- Confirm whether labels exist, are partial, or absent
- If weak labels only, define proxy evaluation method

3. Baseline set
- Rule-based threshold baseline
- Simple statistical baseline

4. Validation and alert quality
- Evaluate precision at alert budget
- Time-to-detect and duplicate-alert rate
- False-alarm analysis by regime

5. Operations and fallback
- Alert triage workflow and owner
- Suppression/cooldown rules
- Fail-safe behavior if model degrades

## Output format

- Anomaly definition and scope
- Label/evaluation strategy
- Baseline and model comparison
- Alert quality dashboard spec
- Triage and fallback policy

## Project adaptation notes

- Add SLA targets for alert response when needed.
- Add hard alert budget constraints to reduce operator overload.
- Add root-cause capture fields for learning loops.
