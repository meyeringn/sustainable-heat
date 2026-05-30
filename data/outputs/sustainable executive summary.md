# SustAInable — Executive Summary

**Report Date:** May 30, 2026
**Decision Threshold:** 0.3
**Model:** XGBoost Supervised Classification
**Produced by:** Nico Meyering, MPA — [github.com/meyeringn/sustainable-heat](https://github.com/meyeringn/sustainable-heat)

-----

## What SustAInable Found

SustAInable scored **2,500 ZIP codes** across 5 U.S. regions for elevated heat illness risk.

Of those, **2,060 ZIP codes** (82.4%) are flagged for proactive public health intervention.

|Priority Tier|ZIP Codes|Recommended Action                                          |
|-------------|---------|------------------------------------------------------------|
|🔴 Critical   |1084     |Immediate — coordinate emergency cooling and health services|
|🟠 High       |565      |Deploy cooling resources before next heat event             |
|🟡 Elevated   |411      |Proactive outreach within 30 days                           |
|🟢 Monitor    |440      |Include in seasonal planning                                |

-----

## Model Performance

|Metric   |Value|What It Means                                                 |
|---------|-----|--------------------------------------------------------------|
|Recall   |95.7%|SustAInable identified 95.7% of high-risk ZIP codes in advance|
|Precision|79.9%|79.9% of flagged ZIP codes were genuinely at elevated risk    |
|F2-Score |0.920|Primary metric — recall weighted twice as heavily as precision|
|AUC-ROC  |0.791|Overall model discrimination (1.0 = perfect, 0.5 = random)    |

-----

## The Core Judgment

In 2023, heat killed **2,415 Americans** — the highest count in 45 years. That number is an undercount.
Missing a high-risk community during a heat wave means preventable deaths.
SustAInable is calibrated to minimize false negatives.

-----

## Next Steps

1. Share your jurisdiction’s data — SustAInable retrains on local records in one session
1. Select your operating threshold — full trade-off curve in outputs folder
1. Import `sustainable_agency_report.csv` directly into outreach planning systems

Contact: **[nicmeyering@gmail.com](mailto:nicmeyering@gmail.com)** · [LinkedIn](https://www.linkedin.com/in/nicolasmeyering)