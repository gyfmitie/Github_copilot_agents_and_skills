---
name: preset-forecasting
description: Optional add-on preset for forecasting projects with lean horizon-aware design and rolling validation.
argument-hint: [target] [horizon] [cadence]
---

# Forecasting Preset (Lean)

## Universal default

Use this preset when the target is time-dependent and you need a fast, defensible forecast baseline.

## Procedure

1. Forecast definition
- Target and horizon
- Update cadence

2. Temporal leakage controls
- Feature availability timing
- No future-value leakage

3. Minimum baselines
- Seasonal naive
- Persistence or moving average

4. Lean validation
- Walk-forward or rolling split
- One primary metric and key regime checks

5. Fallback
- Define low-confidence fallback action

## Output format

- Forecast spec
- Baseline table
- Lean backtest summary
- Fallback note

## Project adaptation notes

- Add uncertainty intervals if decisions are risk-sensitive.
- Add seasonality segments for your domain.
