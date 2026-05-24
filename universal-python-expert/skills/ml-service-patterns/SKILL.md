---
name: ml-service-patterns
description: Implement practical ML training and inference patterns with reproducibility and drift awareness.
argument-hint: [task] [inference mode] [latency constraints]
---

# ML Service Patterns

## Procedure

1. Define baseline model and minimum acceptable performance.
2. Separate training, evaluation, and inference pipelines.
3. Lock feature transformations to avoid train/serve skew.
4. Track model/data versions and experiment metadata.
5. Define calibration, confidence, and fallback behavior.
6. Add drift and data quality monitoring strategy.

## Output format

- Baseline and candidate strategy
- Training/evaluation protocol
- Inference contract
- Monitoring and retraining triggers
- Risk and fallback plan
