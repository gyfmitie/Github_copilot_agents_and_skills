---
name: Building Energy Features & Weather Engineering
description: Granular standards for weather feature selection, occupancy modeling, and feature engineering in building energy forecasting.
applyTo: "**/*.py"
---

# Building Energy Features & Weather Engineering

## Weather Feature Hierarchy for Building Energy

### Tier 1: Non-negotiable (every model)
1. **Dry bulb temperature (°C)**
   - Hourly or half-hourly, direct measurement
   - Required for heating/cooling load calculation
   - SAP and CIBSE design use 15.5°C base for degree-days
   - Check units explicitly: °C not °K or °F

2. **Solar irradiance (W/m²)**
   - Global horizontal irradiance (GHI) at minimum
   - If building has significant glazing (>20% of wall area), separate by façade orientation
   - Decompose into direct normal (DNI) and diffuse horizontal (DHI) if available
   - Solar gains ∝ window area × g-value × irradiance decomposed by orientation

3. **Relative humidity (%)** or **dew point (°C)**
   - Needed for latent load and dehumidification energy
   - Check physical consistency: dew point must be ≤ dry bulb
   - Humidity ratio (kg/kg) = 0.622 × e_s(T_dew) / (P_atm − e_s(T_dew))
     where e_s is saturation vapor pressure
   - Flag any RH = 100% sustained for hours (sensor saturation or fogging)

### Tier 2: Strongly recommended (most buildings)
4. **Wind speed (m/s)**
   - Infiltration loss ∝ (ACH) × wind speed² at low speeds, wind speed at higher speeds
   - Critical for naturally ventilated or mechanically ventilated buildings with poor sealing
   - Check for spurious zero values; wind data should have natural variation
   - If location is coastal or exposed, wind direction also matters

5. **Atmospheric pressure (hPa)**
   - Small but measurable effect on heating load via infiltration
   - Required for accurate humidity ratio and latent load calculation
   - Less critical than temperature and humidity

### Tier 3: Optional (if available and valid)
6. **Precipitation (mm/h or mm/day)**
   - Indirect effect: reduces solar gain (cloud cover), affects occupancy (weather-driven behavioral load)
   - Do not use as direct feature; derive cloud cover or "poor weather" indicator instead
   - Useful if building has drainage loads (sump pumps, dehumidification)

7. **Cloud cover (oktas or fraction)** 
   - More useful than raw precipitation
   - Modulates solar irradiance; check consistency with GHI and wind
   - Can be derived from GHI if measured irradiance is available

## Weather Feature Validation Checklist

### Data quality
- [ ] No missing values > 1 consecutive hour (or document interpolation method)
- [ ] Temperature range plausible: −15 to +35°C for UK (flag extremes)
- [ ] Humidity 0–100% (or 0–100 oktas)
- [ ] Solar irradiance 0–1500 W/m² (max ~1367 at Earth's distance from sun)
- [ ] Wind speed 0–30 m/s typical (flag > 30 m/s; record as storms or sensor fault)
- [ ] Pressure 980–1050 hPa for UK
- [ ] No abrupt jumps in any feature (spike detection)

### Seasonal plausibility
- [ ] Winter (Dec–Feb) temperatures centered on 5°C, with cold snaps to −10°C
- [ ] Summer (Jun–Aug) temperatures centered on 15°C, with peaks to 25°C+
- [ ] Solar irradiance peaks (noon, summer): 800–900 W/m²; (winter) 300–400 W/m² at solar noon
- [ ] Humidity typically 60–80% in winter, 40–70% in summer
- [ ] Seasonal distribution matches 30-year climate normals for the region

### Source and provenance
- [ ] Document source: Met Office, PVGIS, local station, etc.
- [ ] Note distance from building and elevation difference
- [ ] Record any gap filling or interpolation method
- [ ] Flag any data from years mixed without seasonal normalization
- [ ] If using reanalysis (ECMWF, MERRA), apply bias correction against local observations

## Building Occupancy & Schedule Features

### Core occupancy signals
1. **Actual occupancy** (if measured)
   - Badge swipes, CO2-based count, motion sensors, WiFi probe data
   - Validate against expected schedule; flag unexplained occupancy patterns
   - Weekday, weekend, and holiday schedules must be explicit

2. **Occupancy proxy** (if direct measurement unavailable)
   - Plug load (sub-metered if possible)
   - Lighting load (note that occupancy may not track lighting exactly)
   - Derived from energy consumption itself (circular; use only for out-of-sample proxy)

3. **Scheduled occupancy** (from building operations)
   - Opening hours: M–F 08:00–18:00, Sat closed, Sun closed (example)
   - Holidays and special closures: Bank holidays, summer shutdown, COVID lockdowns
   - School holidays (if applicable)
   - Shift changes and staggered hours

### Feature engineering for occupancy
- **Occupancy flag**: 1 if occupied, 0 if closed or night hours
- **Time in working day**: 0–8 hours from start of occupancy (captures ramp-up)
- **Occupancy density**: Occupants per 100 m² (if head count available)
- **Deviation from normal schedule**: Flag unusual occupancy (emergency, deep clean, etc.)

### Schedule validation
- [ ] Occupancy hours match building control system documentation
- [ ] Holidays are correctly labeled (check against UK Bank Holiday calendar + local exceptions)
- [ ] Occupancy ramp-in and ramp-out periods are documented (e.g., ±30 min before/after official hours)
- [ ] Any unscheduled closures (COVID, maintenance) are explicitly flagged in training data

## Building Systems & Thermal Characteristics

### Required parameters (from design or survey)
- **Building area (m²)**: Gross internal area (GIA) or Net usable area (NUA)
- **Window area (m²)** and **orientation breakdown**: N, NE, E, SE, S, SW, W, NW
- **Solar transmittance (g-value / SHGC)**: From Part L schedules or window spec sheets
- **Wall U-value (W/m²K)**: Outer walls, inner surfaces
- **Roof U-value (W/m²K)**: Top surface (heaviest solar gain in summer)
- **Floor U-value (W/m²K)**: If not well insulated, ground source can be significant
- **Infiltration rate**: Air changes per hour (ACH) from blower door test (ideal) or Part L default
- **Thermal mass**: Estimate from construction (lightweight ~50 kJ/m²K; heavyweight ~100+ kJ/m²K)

### HVAC systems (if applicable)
- **Heating**: Boiler type (condensing gas, oil), capacity (kW), efficiency η
- **Cooling**: Chiller or air-cooler, capacity (kW), coefficient of performance (COP)
- **Ventilation**: Type (natural, mechanical extract, balanced with recovery)
  - If mechanical, heat recovery efficiency (%)
  - Extract/supply rates (m³/s or ACH)
- **Hot water**: Storage volume (L), immersion backup, solar thermal (if present)

### Controls and setpoints
- **Heating setpoint (°C)**: Typical 20–21°C for occupied hours
- **Cooling setpoint (°C)**: Typical 21–24°C if active
- **Night setback**: What temperature at night/weekends (e.g., 16°C)
- **Dead band (°C)**: Hysteresis between heating/cooling activation

All parameters must be sourced: measured from BMS, calculated from building survey, or standard assumption (SAP default).

## Feature Derivation & Transformations

### Recommended derived features
1. **Heating degree-days (HDD)**
   - HDD = max(0, T_base − T_daily_avg)
   - UK standard: T_base = 15.5°C (SAP)
   - Cumulative or daily, document which
   - Example: if daily avg = 10°C, HDD = 5.5°C

2. **Cooling degree-days (CDD)**
   - CDD = max(0, T_daily_avg − T_base)
   - T_base = 21°C common for buildings (site-specific may be justified)
   - Only relevant if cooling is present

3. **Solar gains by orientation**
   - GHI (global horizontal) for horizontal surfaces (roof, skylights)
   - Apply cosine factor for vertical surfaces by orientation
   - Example: S-facing vertical surface receives ~65% of GHI at noon in summer (latitude ~52°N)
   - If detailed façade areas by orientation: Solar gain = Σ(window area × orientation factor × g-value × irradiance decomposed by orientation)

4. **Humidity ratio (kg/kg)**
   - From dry bulb T and dew point T_dew or RH
   - Use for latent load: Latent energy ∝ (humidity ratio) × mass flow rate
   - ASHRAE equations recommended; simple approximation: ω ≈ 0.622 × e / (P − e) where e is vapor pressure

5. **Wind-driven infiltration**
   - Infiltration loss ∝ ACH × (stack effect + wind effect)
   - Wind effect ≈ (wind speed)^n, where n = 0.5–2.0 depending on building tightness
   - Conservative: use (T_indoor − T_outdoor) × ACH × wind speed^0.5 as proxy

### Cyclical features (for time-of-year, time-of-day)
- **Hour of day**: 0–23, encode as sin(2π × h / 24) and cos(2π × h / 24) to preserve circularity
- **Day of year**: 1–365, encode as sin(2π × d / 365) and cos(2π × d / 365)
- **Day of week**: 0–6, one-hot encode (7 binary features)

### One-hot encoding for schedules
- **Holiday flag**: UK-specific (Easter, Christmas, Bank Holidays)
- **Season flag**: Winter (Dec–Feb), Spring (Mar–May), Summer (Jun–Aug), Autumn (Sep–Nov)
- **Weekday/weekend**
- **School term flag** (if applicable)

## Feature Selection & Validation

### Multicollinearity checks
- Temperature and degree-days are perfectly collinear; use one or the other, not both
- Solar irradiance (GHI) and cloud cover are correlated; include both only if model interprets them separately
- Wind speed and temperature often weakly correlated; jointly acceptable
- Time-of-day and solar irradiance are correlated; both should contribute independently to model fit

### Leakage detection
**Do NOT use these in training if they are unavailable at prediction time:**
- Actual measured occupancy (if real-time occupancy is not available in deployment)
- HVAC setpoint or operating mode (unless it is pre-set and fixed)
- Future weather (always use only current and lagged features)
- Load from other buildings (unless those buildings are measured in deployment)

### Feature importance and linearity
- Inspect partial dependence plots for each feature
- Temperature should show strong monotonic increase in heating load (kW) per °C below setpoint
- Solar gains should increase load proportionally in summer (and reduce heating in winter)
- Occupancy should step up during working hours
- If any feature is non-monotonic or has suspicious slope, revisit data quality or feature definition

## Summary: Minimal Valid Feature Set for Building Energy

At minimum, a defensible model includes:
1. **Temperature** (hourly)
2. **Solar irradiance** (global horizontal, hourly)
3. **Humidity** (RH or dew point, hourly) or **humidity ratio** (derived)
4. **Wind speed** (hourly)
5. **Occupancy flag** (from schedule or measured)
6. **Building thermal parameters** (area, U-values, window g-value, ACH)
7. **Time of week** (cyclic encoded)
8. **Heating/cooling setpoints** (fixed or from BMS)

Plus validation on separate seasons and regimes (heating vs. cooling, occupied vs. unoccupied).

**Anything less risks overlooking material physics.**
