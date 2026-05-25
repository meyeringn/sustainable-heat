# SustAInable — Development Roadmap

> Predicting neighborhood-level heat illness risk before the crisis, not after.

This roadmap tracks SustAInable from its current state (fully designed,
seeking partners) through pilot deployment. Each phase has a clear goal,
defined outputs, and identified resource needs.

---

## Current Status: Phase 1 Complete ✅

The model architecture, feature schema, data strategy, equity framework,
and asymmetric error cost structure are fully designed and documented.
The design memo is available in this repository.

**What's needed to move forward:** A data engineering collaborator,
ML practitioner, or fellowship/funding opportunity to support Phase 2.

---

## Phase 1 — Design & Framework ✅ Complete
**Goal:** Define the problem, the model, and the equity principles
before writing a single line of code.

- [x] Problem scoping: identified the gap between NOAA HeatRisk
(when) and CDC HHI (who) — neither answers "which ZIP codes
this time"
- [x] Feature schema: 20+ input variables across structural
vulnerability, health burden, and meteorological data
- [x] Label definition: ZIP-level binary classification tied to
NOAA HeatRisk Level 3+ events and ED visit baselines
- [x] Asymmetric error cost framework: false negatives
(missed high-risk ZIPs) defined as categorically worse
than false positives
- [x] Data source inventory: 10 publicly accessible datasets
identified, documented, and linked
- [x] Algorithm selection: XGBoost with SMOTE, class weighting,
and recall-prioritized threshold (0.30)
- [x] Evaluation design: AUC-ROC ≥ 0.85, Recall ≥ 0.80,
baseline comparison to CDC HHI alone (AUC ≈ 0.72–0.74)
- [x] Design memo published

---

## Phase 2 — Data Assembly & Exploration 🔄 In Progress
**Goal:** Pull real data from identified sources, understand its
structure, and confirm the feature schema holds against actual records.

- [ ] Download and clean CDC Heat and Health Index (ZCTA level)
- [ ] Download and clean ACS 5-Year Estimates
(poverty, housing, disability prevalence)
- [ ] Download and clean CDC PLACES
(chronic disease prevalence by ZCTA)
- [ ] Pull NOAA Climate Data Online historical heat event records
- [ ] Connect to NOAA HeatRisk API (forecast data)
- [ ] Acquire Landsat 8/9 land surface temperature data
via Google Earth Engine
- [ ] Pull NSSP ED visit records for heat illness label construction
(ICD-10 T67.x codes)
- [ ] Build unified training dataset: one row per ZCTA per heat event,
2010–2021
- [ ] Publish exploratory data analysis notebook (EDA)
- [ ] Validate label distribution: confirm class imbalance
and SMOTE parameters

**Outputs:** Clean training dataset · EDA notebook ·
Data dictionary (see `/data`)

---

## Phase 3 — Prototype Model 🔲 Planned
**Goal:** Train an initial XGBoost model on historical data,
evaluate against holdout set, and publish results transparently.

- [ ] Train XGBoost baseline model on 2010–2021 data
- [ ] Evaluate on holdout set: 2022–2024
(includes 2022 Pacific Northwest dome, 2023 Texas record heat,
2024 Phoenix multi-week event as stress tests)
- [ ] Generate SHAP feature contribution summaries
— so communities can see *why* a ZIP was flagged
- [ ] Publish Precision-Recall curve and threshold selection rationale
- [ ] Compare against CDC HHI baseline (target: AUC improvement ≥ 0.10)
- [ ] Document failure cases: where does the model underperform
and why?

**Outputs:** Trained model · Evaluation report ·
SHAP explainability outputs · Published notebook

---

## Phase 4 — Pilot Partner 🔲 Planned
**Goal:** Run SustAInable against a real approaching heat event
with a municipal or public health partner and validate predictions
against observed outcomes.

- [ ] Identify pilot partner: municipal OEM, public health department,
or community-based organization
- [ ] Establish data sharing agreement for real-time ED visit data
- [ ] Connect live NOAA HeatRisk forecast feed
- [ ] Run shadow deployment: generate predictions without
operational use, compare to outcomes
- [ ] Debrief with partner: what did the model catch?
What did it miss? What would deployment have changed?
- [ ] Publish pilot results openly

**Target partners:** Philadelphia Department of Public Health ·
Philadelphia OEM · CBOs serving Disabled and elderly residents ·
Any municipal health department in a high-heat-risk metro

---

## Phase 5 — Deployment & Scale 🔲 Future
**Goal:** Move from shadow deployment to operational use
in at least one city, with a path to multi-city scale.

- [ ] Build a lightweight dashboard for OEM and
public health department users
- [ ] Automate NOAA HeatRisk trigger: model runs automatically
when HeatRisk Level 3+ is forecast 48–72 hours out
- [ ] Develop community-facing output: plain-language risk summaries
per ZIP that CBOs can share with residents
- [ ] Document replication guide for other cities
- [ ] Explore multi-city data consortium:
cities share anonymized ED records, all receive improved predictions

---

## How to Help

If you work in public health, climate equity, emergency management,
or civic tech — or if you're a data engineer or ML practitioner
interested in this problem — I want to hear from you.

**I am actively looking for:**
- Public health departments, OEMs, or CBOs interested in a pilot
- Data engineers or ML practitioners to collaborate on Phases 2–3
- Fellowship or funding opportunities to support full development

**Contact:** [LinkedIn](https://www.linkedin.com/in/nicolasmeyering)
· meyeringn@gmail.com
