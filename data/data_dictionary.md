# Data Dictionary — SustAInable

One row in the training dataset = one ZIP Code Tabulation Area (ZCTA)
during one NOAA HeatRisk Level 3+ heat event.

---

## Structural Vulnerability Features

| Column Name | Data Type | Description | Source |
|---|---|---|---|
| zcta | string | ZIP Code Tabulation Area identifier | US Census |
| poverty_rate | float | % of residents below federal poverty line | ACS 5-Year |
| pct_renters | float | % of housing units that are renter-occupied | ACS 5-Year |
| pct_housing_pre1980 | float | % of housing units built before 1980 | ACS 5-Year |
| disability_prevalence | float | % of residents with any disability | ACS 5-Year |
| pct_elderly | float | % of residents age 65+ | ACS 5-Year |
| pct_no_ac | float | % of housing units without air conditioning | CDC HHI |
| green_space_pct | float | % of land area classified as vegetation | NLCD 2021 |

---

## Health Burden Features

| Column Name | Data Type | Description | Source |
|---|---|---|---|
| cardiovascular_prev | float | % of adults with cardiovascular disease | CDC PLACES |
| copd_prev | float | % of adults with COPD | CDC PLACES |
| obesity_prev | float | % of adults with obesity | CDC PLACES |
| diabetes_prev | float | % of adults with diabetes | CDC PLACES |
| prior_heat_ed_rate | float | Heat illness ED visits per 10,000 residents (3-year baseline) | NSSP |

---

## Environmental / Meteorological Features

| Column Name | Data Type | Description | Source |
|---|---|---|---|
| land_surface_temp | float | Average land surface temperature (°C) | Landsat 8/9 |
| uhi_intensity | float | Urban heat island intensity vs surrounding rural area | Landsat 8/9 |
| impervious_surface_pct | float | % of land area that is impervious (concrete, asphalt) | NLCD 2021 |
| heatrisk_level | integer | NOAA HeatRisk forecast level at event onset (0–4) | NOAA HeatRisk |
| max_temp_anomaly | float | Max temperature departure from 30-year normal (°F) | NOAA CDO |
| humidity_anomaly | float | Humidity departure from 30-year normal | Copernicus ERA5 |
| event_duration_days | integer | Number of consecutive days at HeatRisk Level 3+ | NOAA CDO |
| nighttime_low_temp | float | Average overnight low temperature during event (°F) | NOAA CDO |

---

## Label

| Column Name | Data Type | Description | Source |
|---|---|---|---|
| elevated_heat_illness | integer | 1 = ZCTA experienced ≥ 2x baseline ED visits for heat illness (ICD-10 T67.x) during event; 0 = did not | NSSP / CDC WONDER |

---

## Notes

- Unit of analysis: one ZCTA × one heat event = one training row
- Training set covers heat events 2010–2021
- Holdout set covers 2022–2024 (unseen during training)
- Class imbalance expected: elevated illness ZCTAs are the minority class
- SMOTE oversampling applied during training to address imbalance
