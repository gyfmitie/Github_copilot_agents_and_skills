---
name: Building Energy Forecasting - Core Framework
description: Rigorous standards for building energy prediction models with weather integration, time-series validation, and CIBSE/Part L compliance.
applyTo: "**/*.py"
---

# Building Energy Forecasting Framework

## Regulatory and Standards Context

All tools must support compliance reporting under:
- **CIBSE TM54**: Building energy performance assessment methodology
- **Part L Building Regulations**: Energy efficiency requirements (2023 amendments)
- **SAP (Standard Assessment Procedure)**: Domestic energy rating
- **SBEM (Simplified Building Energy Model)**: Non-domestic energy rating
- **ISO 50001**: Energy management systems
- **M&V Protocols**: IPMVP, ASHRAE 14, EN 15603

Always document which standards the model addresses and which it does not.

## Objective Framing for Building Energy

Every forecast or assessment must specify:
- **Building type and classification**: Domestic, office, retail, industrial, mixed-use
- **Energy vectors**: Electricity (kWh), gas (kWh or m³), heating oil, renewable inputs
- **Boundary definition**: Whole building, sub-metered zones, individual end-uses
- **Decision use**: Compliance certification, operational control, retrofit appraisal, billing validation
- **Regulatory context**: Does this support Part L reporting, EPD, DEC, or internal energy management?

Reject vague framing like "optimize energy" without specifying building type, vectors, and decision impact.

## Weather Data Requirements

### Preferred sources (in order)
1. **CIBSE Design Summer Year (DSY)** or **Test Reference Year (TRY)** for specific location
2. **UK Met Office observations** (hourly, quality-controlled)
3. **PVGIS/PVLIB or ECMWF** reanalysis with calibration
4. **Local weather station** if available and quality-assured

### Essential weather features
- **Dry bulb temperature (°C)**: Direct hourly measurement, not derived
- **Relative humidity (%)** or **dew point (°C)**: Required for humidity ratio and latent load
- **Solar irradiance (W/m²)**: Global horizontal (GHI), direct normal (DNI), and diffuse horizontal (DHI)
  - Separate by window orientation if building-specific solar gain is material
  - Flag missing or reconstructed irradiance periods
- **Wind speed and direction (m/s, degrees)**: Critical for infiltration and free cooling
- **Atmospheric pressure (hPa)**: For density corrections in VAV systems
- **Precipitation (mm/h)**: For drainage loads and humidity impacts

### Weather data validation
- Check for sensor failures, spikes, and physically impossible combinations (e.g., RH > 100%)
- Flag gaps > 1 hour and interpolation method used
- Compare seasonal patterns against CIBSE design conditions and 30-year climate normals
- Reject weather data from different years mixed without explicit seasonal adjustment
- Document any weather station distance from building and elevation difference

### No substitution without explicit justification
- Do not use generic UK climate without site-specific validation
- Do not mix data from different stations without documented bias correction
- Do not use weather forecasts as training data for historical model evaluation

## Time-Series Data Handling

### Temporal structure requirements
- **Sampling interval**: Explicitly state (15-min, hourly, daily) and enforce consistency
- **Timezone**: Always use local time for building operations; record UTC offset
- **Daylight Saving Time (DST)**: Document handling around DST transitions (clocks change 2x per year in UK)
- **Leap seconds and time jumps**: Flag and handle explicitly

### Validation checks before modeling
- Check for missing timestamps and gaps
- Detect and remove duplicate records
- Flag out-of-order timestamps
- Verify monotonic time index (no going backwards)
- Document any data exclusion periods with reason (e.g., "building closed for refurbishment weeks 12-15")

### Commissioning and fault periods
Explicitly separate and exclude:
- First 4-12 weeks after system commissioning or major controls retrofit
- Known equipment faults and maintenance windows
- Building closure periods (holidays, COVID lockdowns)
- Major envelope changes (window replacement, insulation retrofit)

Do not model these periods as training data unless explicitly justified.

## Building-Specific Features

### Occupancy and schedule features
- **Occupancy count** or **occupancy proxy** (CO2, motion sensors, badge swipes)
  - Must distinguish working hours from out-of-hours baseline
  - Weekend and holiday schedules must be explicit
  - School terms, summer closures, shutdown weeks must be labeled
- **Lighting and equipment schedules**: Derive from sub-metered data or controls logs where possible
- **HVAC setpoints and operating mode**: Extract from BMS if available
- **Known events**: Bank holidays, special closures, emergency shutdowns

### Thermal characteristics
- **Building fabric**: U-values by element (walls, roof, floor, windows)
  - Reference SAP worksheet or Part L calculations where available
  - Note any known insulation improvements and dates
- **Thermal mass**: Estimated from construction type and area
- **Infiltration rate (ACH)**: From blower door test, Part L default, or inverse model fitting
- **Window area and solar gain**: Total window area, orientation, g-values (SHGC)

### Systems and end-use breakdown
- **Heating system**: Boiler type, capacity, efficiency, fuel type
- **Cooling/air conditioning**: Type, capacity, hours of operation
- **Hot water system**: Storage capacity, immersion backup, solar fraction
- **Lighting power density**: W/m² by zone if available
- **Plug loads and appliances**: Estimate from metering or Part L defaults

All physical parameters must be documented with source (measured, design, standard assumption).

## Feature Engineering for Building Energy

### Derived features (strictly validated)
- **Degree-days**: Base temperature 15.5°C (SAP standard) or site-specific if justified
  - CDD: Cooling degree-days, base 21°C (if cooling is material)
  - Use CIBSE data where available; document base temperature choice
- **Solar gains**: Decompose GHI into direct and diffuse; apply orientation factors
- **Wind chill factor**: (temperature, wind speed) for infiltration-driven heating
- **Humidity ratio (kg/kg)**: From dry bulb and dew point for latent load assessment
- **Time of week and time of day**: Hour, day of week, week of year (cyclic encoding recommended)
- **Holiday and school term flags**: UK-specific calendar

### Feature validation
- No look-ahead bias: do not use future weather in current prediction
- No leakage: occupancy, thermostat setpoint, or controls state should not be used if unavailable in deployment
- Justify any feature that has high correlation with time-of-day or seasonality alone
- Check for multicollinearity, especially among weather features (wind speed and temperature often correlated)

## Time-Series Validation Protocol

### Validation strategy (mandatory for building energy)
- **Time-based split**: Train on earlier periods, validate on later periods (no shuffle)
- **Minimum training period**: 12 months (to capture seasonal variation)
- **Test period**: Minimum 1-3 months (at least one season representative of future deployment season)
- **Season-specific holdouts**: Validate separately on winter, summer, and shoulder season data

### Regime-level performance assessment
Evaluate model separately by:
- **Occupied vs. unoccupied hours**: Buildings often have distinct load profiles
- **Heating season (Oct-Mar) vs. summer (Jun-Aug)**
- **Peak load hours vs. off-peak**: Different physics apply
- **Weekday vs. weekend**: Occupancy-driven differences
- **Weather regimes**: Cold snaps, heat waves, mild weather, high wind events

Do not rely on global RMSE or MAE; always include per-regime error decomposition.

### Baseline comparison (mandatory)
Compare against:
- **Degree-day model**: Energy ∝ (T_indoor − T_outdoor) × occupied hours
- **Weekly profile + temperature**: Average consumption per day of week + heating/cooling adjustment
- **SAP calculation**: If Part L compliance is relevant, show model vs. SAP estimate and explain differences

### Uncertainty and bounds
- Report **prediction interval** (e.g., 68% and 95% bounds, not just point estimates)
- Document calibration of uncertainty: Is 95% interval actually covering 95% of holdout errors?
- Identify regimes where model confidence is low (e.g., extreme weather, building mode changes)

## Regulatory and Reporting Requirements

### Part L and SAP alignment
- If model is used for Part L compliance reporting, explicitly state assumptions that differ from SAP
- Document any regulatory approval or acceptance of simplified methods
- Keep audit trail of model changes and validation results

### Energy Performance Certificate (EPC) context
- For EPCs, models must be consistent with SBEM or SAP methodology
- If using ML instead of SAP defaults, document why and seek building control approval
- Maintain records of building characteristics used (fabric, systems, occupancy)

### Measurement & Verification (M&V)
- If model is used to assess energy savings (retrofit, controls upgrade), follow IPMVP guidelines
- Specify: adjustments (weather, occupancy, operational), persistence of savings, confidence level
- Use ASHRAE Guideline 14 or EN 15603 for baseline establishment and savings calculation

## Documentation and Handover

Every forecast model must include:
- **Model card**: Building type, date range, energy vectors, key assumptions, performance by regime
- **Weather data provenance**: Source, quality checks, any gaps and interpolation method
- **Feature list**: Physical meaning, units, source (measured, derived, standard assumption)
- **Validation results**: RMSE/MAE by season and regime, uncertainty bounds, baseline comparison
- **Regulatory status**: Which standards it aligns with, known deviations, approval status
- **Retraining and monitoring plan**: How often to retrain, what triggers a model update

## Response Behavior for Assistant

When evaluating building energy tools or proposals:
1. **Objective**: Confirm building type, energy vectors, regulatory context, and decision use
2. **Data**: Assess weather source quality, building characteristics completeness, time-series integrity
3. **Method**: Check for proper time-based validation, regime-level analysis, baseline comparison
4. **Standards**: Verify alignment with CIBSE, Part L, SAP, or IPMVP as relevant
5. **Uncertainty**: Demand prediction intervals and calibration checks, not point estimates alone
6. **Deployment**: Confirm model handles new occupancy patterns, system changes, and out-of-distribution weather

Red flags:
- Global error metric only (no per-season or per-regime breakdown)
- No baseline comparison
- Weather data sourced generically without site validation
- Training and test data mixed (non-time-based split)
- No documented handling of building closure, commissioning, or major retrofits
- Regulatory claims without explicit standard alignment
