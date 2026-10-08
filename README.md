# Raghad-Tamweel-Advanced-Machine-Learning-Methods-SDA-DSC-21١

# Tamweel Lite — Cost-Aware Credit-Risk Review Policy

An end-to-end machine-learning project for predicting **synthetic financing defaults within 90 days**, with time- and customer-based validation, cost-sensitive threshold selection under a **12% review capacity**, and assessment of calibration and interpretability.

**Course:** SDA-DSC-211 — Advanced Machine Learning Methods (SDAIA Academy) **Project:** Individual Five-Day Project

> **Educational use only.** All data is synthetic. A `decision = 1` indicates referral for review in a simulation and does not represent a real approval or rejection decision.


# Tamweel Lite: Final Project

**Decision:** KEEP SINGLE → **Logistic Regression**

| Item | Result |
|---|---|
| Mean OOF AP | **0.392** (fold SD 0.030) |
| Rule | flag if calibrated probability ≥ **0.1223** (raw OOF threshold 0.1689) |
| OOF at threshold | recall **46.9%**, precision 34.3% (84 of 179 defaults) |
| Busiest-period flag rate | 11.7%, within the 12% cap in all 3 periods |
| Challenge batch | 2,500 → 330 above threshold → **300 flagged** |
| Challenge performance | **Not claimed** (no labels) |

![Ensemble comparison](artifacts/day5_ensemble_comparison.png)

## Problem
Choose which applications a limited review team examines. A missed default costs **10×** a false alarm, and review is capped at **12% per period**.

- **Target:** `default_within_90d`, a synthetic default within 90 days after the application.
- **Train:** 10,000 applications (2022–2024), 7.89% positive. **Challenge:** 2,500 unlabeled applications (2025), separate customers.
- **Loss:** `10 × FN + 1 × FP`, in teaching units only.

## Five days
1. **Baseline vs boosting:** `day1_model_comparison.csv`
2. **Leakage audit, time/customer validation, Optuna:** `validation_summary.csv`
3. **Threshold, capacity, regions:** `DECISION_CARD.md`
4. **SHAP, calibration, stability:** `INTERPRETABILITY_REPORT.md`
5. **Worth-it gate, final model, delivery:** `MODEL_CARD.md`, `submission.csv`

*Synthetic educational project. Not for real financing decisions.*

**Developer:** Raghad Aldawsari
**Project type:** Individual capstone project



## Project overview

Tamweel Lite is a machine learning project for credit-risk prediction in a simulated financing environment. The solution estimates the likelihood of customer default within 90 days of application using only information available at submission time. The workflow includes data validation, feature preparation, model training, ensemble learning, probability calibration, threshold optimization, explainability analysis, fairness monitoring, and final prediction generation. The system supports risk-assessment decisions by providing risk scores and review recommendations while keeping final decisions under human oversight.
