# Data Directory — SustAInable

This folder contains processed training data for the SustAInable
heat illness risk prediction model.

## What Goes Here

Raw source data is too large to store in this repository.
All raw datasets are publicly accessible — sources and download
links are documented in the main README.

This folder will contain:
- Cleaned and merged training dataset (2010–2021)
- Holdout dataset (2022–2024)
- Label construction output (ZIP-level binary flags per heat event)
- Feature correlation matrix

## Data Schema

See `data_dictionary.md` in this folder for a full description
of every feature column, its data type, and its source.

## Reproducibility

All data assembly and cleaning steps will be documented
in the `/notebooks` folder once Phase 2 is underway.
No proprietary data is required. Every source is public.
