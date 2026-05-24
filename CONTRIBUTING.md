# Contributing to SustAInable

Thank you for your interest in SustAInable. This project is currently in the design and partner-seeking phase — the model architecture, feature schema, data strategy, and equity framework are fully specified, and implementation is the next step.

Contributions are welcome across several areas.

-----

## What We’re Looking For

### Public Health and Emergency Management Partners

If you work in a municipal Office of Emergency Management, public health department, or community-based organization doing heat response work, we want to talk. SustAInable is designed to produce outputs your team can actually use — a ranked ZIP-code priority list, 48–72 hours before event peak. Your operational constraints should shape how those outputs are delivered.

### ML / Data Engineering

If you have experience with:

- Supervised classification (XGBoost, gradient boosted trees)
- Imbalanced class handling (SMOTE, class weighting, threshold calibration)
- Geospatial feature engineering at the ZCTA level
- SHAP explainability implementation
- Syndromic surveillance data (NSSP, CDC WONDER)

…this project needs you. The design is ready. The build is not.

### Climate Equity and Disability Justice Advocates

SustAInable is a climate equity tool first and a machine learning project second. Disabled people, elderly residents, and low-income communities are the primary intended beneficiaries — and the communities most likely to be missed if the model is wrong. If you work in disability services, heat justice organizing, or environmental justice advocacy, your perspective on how risk scores are communicated and acted on is essential. We want community validators in the loop from the start.

### Data and Epidemiology

If you have experience working with:

- CDC Heat and Health Index data
- NSSP emergency department syndromic surveillance
- NOAA HeatRisk API integration
- Label construction from aggregate health surveillance records

The most significant data engineering challenge in this project is constructing event-level heat illness labels from datasets that are primarily structured as multi-year aggregates. Help here is high-value.

-----

## How to Reach Out

This project is not yet at the pull request stage. If you’re interested in contributing, please reach out directly:

**Nico Meyering, MPA**
[LinkedIn](https://www.linkedin.com/in/nicolasmeyering) · [nicmeyering@gmail.com](mailto:nicmeyering@gmail.com)

Please include a brief note on your background and how you’d like to be involved. I respond to everyone.

-----

## Equity Commitments

Any implementation of SustAInable will include:

- Stratified error analysis by income quintile and disability prevalence — if the model underperforms for the most vulnerable communities, that is a failure, not a footnote
- SHAP feature contribution summaries published per ZCTA — community organizations can see why a ZIP code was flagged and challenge scores that reflect data gaps rather than current conditions
- Data sparsity treated as a risk signal, not a clean bill of health — ZCTAs with thin historical surveillance data are flagged, not silently assigned low scores
- SustAInable is a targeting aid, not an authority — all outputs are accompanied by confidence intervals and explicit guidance that scores inform, not replace, human judgment

Contributors are expected to uphold these commitments in any work they submit.

-----

## Code of Conduct

This project is committed to a welcoming environment for everyone, with particular attention to Disabled contributors, chronically ill community members, and people in communities most exposed to heat illness risk. Harassment of any kind will not be tolerated.

-----

*SustAInable was developed through the Equitech Futures Civic Tech Institute, CTI 2026 Cohort.*
