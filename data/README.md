# Data Directory

This folder contains raw and processed datasets used in SustAInable.

All data sources are publicly available. No proprietary data is required
to reproduce this project.

Raw files are too large to store in this repository. Download links and
instructions for each dataset are documented below.

-----

## How This Folder Is Organized

```
data/
├── raw/ ← Original files downloaded directly from source
├── processed/ ← Cleaned, merged, and analysis-ready datasets
└── README.md ← This file
```

Raw files are never modified. All cleaning and transformation happens
in the `/notebooks` directory and outputs to `/processed`.

-----

## ⬇️ Data Downloads

### 1. CDC PLACES: Local Health Data ← START HERE

- **Used for:** Chronic disease prevalence by ZCTA (diabetes, obesity, COPD, etc.)
- **Provider:** CDC Division of Population Health
- **Direct download (Google Drive):** <https://drive.google.com/file/d/1kfCDHdr-bPHX9RAUSERfxaWidkSNCP_E/view?usp=drive_link>
- **Original source:** <https://www.cdc.gov/places>
- **Save as:** `data/raw/cdc_places_zcta.csv`
- **Format:** CSV
- **Notes:** Download the ZCTA-level file. Key measures: `CSMOKING`,
`OBESITY`, `DIABETES`, `CHD`, `COPD`. Filter to US ZCTAs only.

-----

### 2. CDC Heat & Health Index (HHI)

- **Used for:** Structural vulnerability scores by ZCTA
- **Provider:** CDC Climate and Health Program
- **Access:** <https://ephtracking.cdc.gov/DataExplorer>
- **Save as:** `data/raw/cdc_hhi_zcta.csv`
- **Format:** CSV
- **Notes:** Primary source for baseline vulnerability scores per ZIP code.
Download at ZCTA level. Used in both feature engineering and as a
baseline model comparison (standalone HHI produces AUC ≈ 0.72–0.74).

-----

### 3. American Community Survey (ACS) 5-Year Estimates

- **Used for:** Poverty rate, housing age, disability prevalence, renter rate
- **Provider:** U.S. Census Bureau
- **Access:** <https://data.census.gov>
- **Save as:** `data/raw/acs_zcta.csv`
- **Format:** CSV
- **Notes:** Use the most recent 5-year estimate available. Key tables:
- `B17001` — Poverty status
- `B25034` — Year structure built (housing age proxy)
- `B22010` — Disability status
- `B25003` — Tenure (owner vs. renter)

Pull at ZCTA level. Match to ZCTA using GEOID field.

-----

### 4. NOAA Climate Data Online (CDO)

- **Used for:** Historical temperature and heat event records
- **Provider:** NOAA National Centers for Environmental Information (NCEI)
- **Access:** <https://www.ncdc.noaa.gov/cdo-web/>
- **Save as:** `data/raw/noaa_cdo_daily.csv`
- **Format:** CSV
- **Notes:** Requires free account to download. Pull daily summaries
(GHCND dataset). Filter for summer months (June–September).

-----

### 5. NOAA HeatRisk

- **Used for:** Forecast heat danger level (0–4 scale) per geographic area
- **Provider:** NOAA Weather Prediction Center
- **Access:** <https://www.wpc.ncep.noaa.gov/heatrisk/>
- **Save as:** `data/raw/noaa_heatrisk.csv`
- **Format:** GeoJSON / Shapefile / API
- **Notes:** HeatRisk Level 3+ triggers model prediction.

-----

### 6. NSSP — National Syndromic Surveillance Program

- **Used for:** Emergency department visit records for heat illness
(label construction — primary outcome variable)
- **Provider:** CDC Center for Surveillance, Epidemiology, and Laboratory
Services (CSELS)
- **Access:** <https://www.cdc.gov/nssp> — Restricted access via BioSense
Platform. Requires data use agreement.
- **Save as:** `data/raw/nssp_heat_ed_visits.csv`
- **Format:** Aggregated CSV
- **Notes:** ⚠️ **This dataset requires a formal data access request.**
Pull heat-related illness ED visits by ZCTA using ICD-10 codes T67.x.
This is the primary outcome variable (Y label).

To request access:
1. Visit <https://www.cdc.gov/nssp/php/onboarding/index.html>
1. Complete the BioSense Platform onboarding
1. Submit a data use request

While NSSP access is pending, Notebook 03 runs automatically in
**proxy mode** using structurally derived labels. The full pipeline
runs end-to-end without NSSP data.

-----

### 7. CDC WONDER — Compressed Mortality File

- **Used for:** Heat-related cause of death records (label validation)
- **Provider:** CDC National Center for Health Statistics (NCHS)
- **Access:** <https://wonder.cdc.gov>
- **Save as:** `data/raw/cdc_wonder_heat_deaths.csv`
- **Format:** CSV (query-based download)
- **Notes:** Use Underlying Cause of Death file. ICD-10 codes X30
and T67.x.

-----

## Data Access Summary

|Dataset |Access Level|Requires Account|Requires DUA|Status |
|---------------|------------|----------------|------------|-----------------------------------|
|CDC PLACES |Public |No |No |✅ Available — see Drive link above |
|CDC HHI |Public |No |No |⬜ Download from ephtracking.cdc.gov|
|ACS 5-Year |Public |No |No |⬜ Download from data.census.gov |
|NOAA CDO |Public |Yes (free) |No |⬜ Download from ncdc.noaa.gov |
|NOAA HeatRisk |Public |No |No |⬜ Download from wpc.ncep.noaa.gov |
|NSSP / BioSense|Restricted |Yes |**Yes** |⏳ DUA application in progress |
|CDC WONDER |Public |No |No |⬜ Download from wonder.cdc.gov |

-----

## ZCTA Boundary Files

All datasets must be joined at the **ZCTA (ZIP Code Tabulation Area)** level.

- **Provider:** U.S. Census Bureau TIGER/Line
- **Access:** <https://www.census.gov/cgi-bin/geo/shapefiles/index.php>
- **Notes:** Use 2020 ZCTA boundaries for consistency across all datasets.

-----

## A Note on the NSSP Data Access Process

The NSSP dataset is the most critical and the most access-restricted.
It is the source of the outcome variable (Y label): elevated heat illness
ED visits per ZCTA.

While NSSP access is pending, the model runs in proxy mode and all
pipeline outputs are demonstration-quality. Numbers will improve
significantly when real NSSP labels replace the proxy.

If you are a public health partner with existing NSSP access and are
interested in collaborating, please reach out:
[meyeringn@gmail.com](mailto:meyeringn@gmail.com)

-----

*SustAInable — Neighborhood Heat Illness Risk Prediction*
*Equitech Futures Civic Tech Institute, CTI 2026*
