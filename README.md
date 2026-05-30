# SustAInable

### Neighborhood-Level Heat Illness Risk Prediction Before the Crisis, Not After

[![Status](https://img.shields.io/badge/status-design%20memo%20%7C%20seeking%20partners-orange)](https://github.com/)
[![Domain](https://img.shields.io/badge/domain-climate%20equity%20%7C%20public%20health-blue)](https://github.com/)
[![Algorithm](https://img.shields.io/badge/algorithm-XGBoost%20supervised%20classification-green)](https://github.com/)
[![Author](https://img.shields.io/badge/author-Nico%20Meyering%2C%20MPA-lightgrey)](https://www.linkedin.com/in/nicolasmeyering)

-----

## The Problem

Last summer, I walked my dog a few blocks from home. I nearly passed out from the heat.

I am a Disabled Philadelphian. I have Congenital Central Hypoventilation Syndrome (CCHS), a condition affecting the autonomic nervous system — the system that regulates breathing, heart rate, and critically, temperature. My wife Ariele has acquired disabilities including chronic illness with autonomic dysfunction. Heat is not an inconvenience for us. It is a physiological threat that our bodies cannot adequately self-regulate against.

We are not alone.

- The official US count for heat-related deaths in 2023: **2,415**
- The estimated real count: **~11,000**
- Heat-related deaths have risen **117% since 1999**
- Disabled people face a **5x relative risk** of heat illness compared to non-disabled people during extreme heat events

The gap between 2,415 and 11,000 is not a measurement error. It is a policy failure — and a data problem.

Two federal tools exist to help cities respond. **NOAA HeatRisk** tells you *when* a dangerous heat event is coming. The **CDC Heat and Health Index** tells you which neighborhoods are *structurally* vulnerable. What neither tool answers is the question that actually matters five days before a heat event:

> *Given this specific forecast, which ZIP codes will see elevated emergency room visits this time?*

**SustAInable answers that question.**

-----

## What It Does

SustAInable is a supervised machine learning model that assigns every US ZIP Code Tabulation Area (ZCTA) a **probability score for elevated heat illness** during an approaching extreme heat event.

It integrates real weather forecasts with neighborhood-level vulnerability data — income, housing stock, disability prevalence, land surface temperature, chronic disease burden, and prior heat illness rates — to give cities, community organizations, and public health departments an actionable targeting tool **before the crisis, not after**.

A city has finite cooling buses, wellness check teams, and emergency supplies. On day one of a heat emergency, a deployment decision cannot be made from a map of generalized structural vulnerability alone. It needs a ranked list: *where do we send resources today?*

SustAInable produces that list.

-----

## Model Design

**Algorithm:** XGBoost (eXtreme Gradient Boosting — supervised binary classification)  
**Unit of analysis:** ZIP Code Tabulation Area (ZCTA)  
**Prediction trigger:** NOAA HeatRisk Level 3+ forecast, ≥ 48 hours in advance

### Inputs (X) — What the Model Learns From

|Category                          |Features                                                                                                                                                                                              |Source                                                    |
|----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------|
|**Structural Vulnerability**      |Poverty rate, % renters, % housing pre-1980, disability prevalence, elderly population %, % without AC, green space coverage                                                                          |ACS 5-Year Estimates; CDC Heat and Health Index; NLCD 2021|
|**Health Burden**                 |Cardiovascular disease prevalence, COPD, obesity, diabetes, prior heat illness ED visit rate (3-year baseline)                                                                                        |CDC PLACES; CDC WONDER; NSSP                              |
|**Environmental / Meteorological**|Land surface temperature, urban heat island intensity, impervious surface coverage, NOAA HeatRisk forecast level, max temperature anomaly, humidity anomaly, event duration, nighttime low temperature|Landsat 8/9; Copernicus ERA5; NOAA CDO; NOAA HeatRisk API |

### Label (Y) — What the Model Predicts

Binary at the ZCTA level, per heat event:

|Label               |Definition                                                                                                                                                                    |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|**1 (Elevated)**    |ZCTA experienced ≥ 2x baseline ED visits per 10,000 residents for heat-related illness (ICD-10 codes T67.x) during a NOAA HeatRisk Level 3+ event lasting ≥ 2 consecutive days|
|**0 (Not Elevated)**|ZCTA did not experience elevated heat illness during the event                                                                                                                |

### Output

For each approaching heat event, SustAInable produces:

- A **probability score (0.00–1.00)** per ZCTA
- A **ranked priority list** of ZCTAs for resource deployment
- A **risk tier**: High (≥ 0.60) · Elevated (0.30–0.59) · Baseline (< 0.30)
- **SHAP feature contribution summaries** per ZCTA — so community organizations and residents can see *why* a ZIP code was flagged, and challenge scores that reflect historical data gaps rather than current conditions

-----

## The Two Errors — and Why They Are Not Equal

Every prediction model makes two kinds of mistakes. SustAInable’s design is shaped by a deliberate asymmetric cost judgment.

|Error Type        |What Happens                                                                           |Cost                                                                                                                                                                                               |
|------------------|---------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|**False Positive**|We flag a ZIP code as high-risk. The neighborhood does not experience elevated illness.|Cooling resources deployed unnecessarily: ~$2,000–$8,000 per ZCTA. Recoverable. No one is harmed.                                                                                                  |
|**False Negative**|We do NOT flag a ZIP code. Elevated illness occurs.                                    |Disabled people, elderly residents, and chronically ill individuals suffer preventable heat illness. Hospitalizations: $15,000–$30,000 per admission. Deaths are irreversible. **Not recoverable.**|


> **A false negative is categorically worse than a false positive. This asymmetry drives every technical decision in SustAInable.**

Specific measures to reduce false negatives:

- **Lower decision threshold:** ZCTAs flagged at score ≥ 0.30, not the default 0.50
- **Class weighting:** Model penalized more heavily for missing an elevated-illness ZCTA
- **SMOTE oversampling:** Synthetic minority oversampling improves model sensitivity to elevated-illness events
- **Recall-prioritized threshold selection:** Maximize recall subject to a minimum precision floor of 0.40 (up to 2.5 false positives per true positive accepted)

-----

## Data Sources

All datasets are publicly accessible. No proprietary data required.

|Dataset                                       |Use                                                     |Provider                         |
|----------------------------------------------|--------------------------------------------------------|---------------------------------|
|CDC Heat and Health Index (HHI)               |Structural vulnerability features at ZCTA level         |CDC Climate and Health Program   |
|ACS 5-Year Estimates                          |Poverty, housing age, disability prevalence, renter rate|US Census Bureau                 |
|CDC PLACES                                    |Chronic disease prevalence by ZCTA                      |CDC Division of Population Health|
|NOAA Climate Data Online (CDO)                |Historical temperature, humidity, heat event records    |NOAA NCEI                        |
|NOAA HeatRisk                                 |Forecast heat danger level (0–4)                        |NOAA Weather Prediction Center   |
|Landsat 8/9 Surface Temperature               |Land surface temperature and urban heat island intensity|USGS / Google Earth Engine       |
|NLCD 2021                                     |Impervious surface and land cover classification        |MRLC Consortium                  |
|Copernicus ERA5 Reanalysis                    |Historical temperature and humidity anomalies           |ECMWF / Copernicus               |
|NSSP (National Syndromic Surveillance Program)|ED visit records for heat illness label construction    |CDC CSELS                        |
|CDC WONDER                                    |Heat-related cause of death records for label validation|CDC NCHS                         |

-----

## Evaluation Design

**Training set:** 2010–2021 (12 years of heat events; excludes post-COVID data disruption)  
**Holdout set:** 2022–2024 (includes 2022 Pacific Northwest dome, 2023 Texas record heat, 2024 Phoenix multi-week event as stress tests)

**Primary metrics:**

- **AUC-ROC** (target: ≥ 0.85) — grounded in Kim et al. (2021) benchmark of AUC = 0.895 for XGBoost heat illness prediction
- **Recall / Sensitivity** (target: ≥ 0.80) — prioritized over precision; missing an elevated-illness ZCTA is not acceptable
- **Precision-Recall AUC** — more appropriate than ROC for imbalanced classes

**Baseline comparison:** CDC HHI structural vulnerability index alone produces AUC ≈ 0.72–0.74. SustAInable must meaningfully outperform this to justify development.

-----

## Who It Serves

|Stakeholder                     |Use Case                                                                                                         |
|--------------------------------|-----------------------------------------------------------------------------------------------------------------|
|Municipal Emergency Management  |Allocate cooling buses and open cooling centers 48–72 hours before event peak                                    |
|Public Health Departments       |Target wellness checks; prioritize elderly and Disabled resident registries for proactive calls                  |
|Community-Based Organizations   |Deploy water and supply distribution to high-risk corridors                                                      |
|Hospitals and Health Systems    |Pre-position emergency capacity in advance of predicted high-volume days                                         |
|Disability Service Organizations|Flag medically fragile clients in high-risk ZCTAs for prioritized check-ins and power outage contingency planning|

-----

## Current Status

> **Phase 2 — EDA in progress** Design memo complete. Exploratory daya analysis notebook now live. Seeking public health, climate equity, and development partners.

SustAInable was developed as a supplemental capstone project through the [Equitech Futures Civic Tech Institute (CTI) 2026](https://www.equitechfutures.com/) cohort. The model architecture, feature schema, data strategy, and equity framework are fully designed. Implementation is the next step.

**I am actively looking for:**

- Public health departments, OEMs, or CBOs interested in a pilot
- Data engineers or ML practitioners interested in building this out
- Climate equity fellowship or funding opportunities to support development
- See 'notebooks/01_eda_heat_vulnerability.ipynb' for Phase 2 data exploration

-----

## Contact

**Nico Meyering, MPA**  
Philadelphia, PA  
[LinkedIn](https://www.linkedin.com/in/nicolasmeyering) · [nicmeyering@gmail.com](mailto:nicmeyering@gmail.com)

*Chairman, Philadelphia Mayor’s Commission on People with Disabilities*  
*VP of Growth & Partnerships, Net Impact Philadelphia*  
*Equitech Futures Civic Tech Institute, CTI 2026*

-----

## Key Citations

- Klinenberg, E. (2002). *Heat Wave: A Social Autopsy of Disaster in Chicago.* University of Chicago Press.
- Kim, Y. et al. (2021). Prediction of heat-related illness using XGBoost in South Korean cities. *International Journal of Environmental Research and Public Health,* 18(4).
- CDC Climate and Health Program. Heat and Health Index Methodology. cdc.gov/climateandhealth
- NOAA Weather Prediction Center. HeatRisk Product Documentation. wpc.ncep.noaa.gov/heatrisk
- CDC WONDER. Compressed Mortality File: Underlying Cause of Death, 1999–2020. wonder.cdc.gov
- Borden, K.A. & Cutter, S.L. (2008). Spatial patterns of natural hazards mortality in the United States. *International Journal of Health Geographics,* 7(64).

-----

*Developed through the Equitech Futures Civic Tech Institute, CTI 2026 Cohort*
