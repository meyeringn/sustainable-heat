# SustAInable — Notebooks

This folder contains the complete ML pipeline for **SustAInable**, a supervised machine learning tool that predicts neighborhood heat illness risk by ZIP Code Tabulation Area (ZCTA).

**Current data status:** All notebooks run on synthetic data generated to mirror the structure of real CDC PLACES, NOAA, and Census vulnerability indicators. Real data ingestion (NSSP/BioSense Platform ED visit records) is pending access approval. To swap in real data, replace the synthetic generation block at the top of Notebook 01 — all downstream notebooks will run without modification.

-----

## Pipeline Overview

|# |Notebook                      |Purpose                                              |Key Output                                                                                |
|--|------------------------------|-----------------------------------------------------|------------------------------------------------------------------------------------------|
|01|`01_eda_synthetic_data.ipynb` |Synthetic data generation + exploratory data analysis|1,200-row ZCTA dataset; feature distributions; correlation matrix                         |
|02|`02_merge_features.ipynb`     |Feature engineering and merge pipeline               |Derived features: vulnerability index, cooling deficit, mobility barrier, income-heat risk|
|03|`03_model_training.ipynb`     |XGBoost model training with SMOTE oversampling       |Trained classifier; ROC curve; confusion matrix at threshold 0.30                         |
|04|`04_shap_explainability.ipynb`|SHAP explainability analysis                         |Feature importance bar chart; per-ZCTA SHAP scatter plots                                 |
|05|`05_model_evaluation.ipynb`   |Threshold analysis + equity audit                    |Precision/recall tradeoff curves; false negative rate by poverty quartile                 |
|06|`06_agency_summary.ipynb`     |Scored ZCTA output for agency partners               |Risk-tiered ZCTA CSV (Critical / High / Moderate / Low)                                   |

-----

## Key Design Decisions

- **Primary metric: Recall.** Missing a high-risk ZCTA (false negative) has a higher cost than flagging a low-risk one (false positive). Recall is prioritized over precision.
- **Decision threshold: 0.30.** Deliberately set below 0.50 to reduce false negatives in public health response.
- **SMOTE oversampling** applied to the training set only to address class imbalance. Never applied to the test set.
- **Equity focus:** Notebook 05 includes an explicit equity audit by poverty quartile. Disabled, elderly, low-income, and unhoused populations are centered throughout the feature design.
- **Explainability:** SHAP values (Notebook 04) make every model prediction auditable — any flagged community can receive a plain-language explanation of *why* it was flagged.

-----

## To Run

1. Open any notebook in [Google Colab](https://colab.research.google.com)
1. Install dependencies (first run only):
   
   ```
   pip install xgboost scikit-learn imbalanced-learn shap matplotlib pandas numpy
   ```
1. Runtime → Run All
1. Notebooks are designed to run independently — each rebuilds the dataset from scratch using the shared random seed (`np.random.seed(42)`)

-----

*SustAInable — Equitech Futures Civic Tech Institute, CTI 2026*  
*Nico Meyering, MPA*