---
name: preset-forecasting
description: Optional add-on preset for forecasting projects with horizon-aware design, temporal leakage prevention, and rolling validation.
argument-hint: [target] [horizon] [cadence]
---

# Forecasting Preset

## Universal default

Use this preset when the target is time-dependent and future values must be predicted.

## Procedure

1. Forecast definition
- Target variable and unit
- Forecast horizon (for example next 24h, next 7d)
- Update cadence (batch, hourly, daily)

2. Temporal data policy
- Enforce timestamp monotonicity and timezone consistency
- Prevent future leakage in features
- Define availability lag for each feature

3. Baseline set
- Seasonal naive baseline
- Moving average or persistence baseline

4. Validation pattern
- Rolling or walk-forward backtesting
- Regime checks (season, weekday/weekend, peak/off-peak)

5. Uncertainty and fallback
- Prediction intervals if decisions depend on risk
- Fallback rule when confidence is low

## Output format

- Forecast spec
- Feature availability map
- Baseline comparison table
- Backtest summary by window
- Uncertainty and fallback summary

## Project adaptation notes

- Add domain seasonality notes (for example weather, holidays, campaign periods).
- Remove interval requirements if policy does not require uncertainty.
- Add cost-weighted metric if under- and over-forecast have different cost.
