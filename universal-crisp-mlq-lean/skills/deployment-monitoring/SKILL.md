---
name: deployment-monitoring
description: Define release strategy, runtime safeguards, drift monitoring, and retraining policy.
argument-hint: [deployment mode] [monitoring KPIs] [retraining trigger]
---

# Deployment and Monitoring

## Universal default

Use this skill when preparing production rollout and operations.
For lean prototyping, keep this as a production-readiness checklist unless deployment is immediate.

## Procedure

1. Serving contract
- Define model input/output schema and versioning.
- Define latency and availability targets.

2. Rollout plan
- Shadow, canary, or phased rollout.
- Rollback conditions and owner.

Lean note:
- If still in prototype stage, define the intended rollout mode without fully implementing it yet.

3. Runtime safeguards
- Input validation and out-of-distribution detection.
- Low-confidence fallback behavior.

4. Monitoring
- Data drift, concept drift, and prediction quality proxies.
- Alert thresholds and incident workflow.

5. Retraining policy
- Time-based and event-based triggers.
- Validation requirements before promotion.

## Output format

- Deployment architecture summary
- Rollout and rollback plan
- Monitoring dashboard spec
- Drift and retraining policy
- Operational risk summary

## Project adaptation notes

- Add SLOs and on-call policy for production systems.
- Remove heavy monitoring for low-risk internal tools.
- Add security and privacy controls for sensitive data.
