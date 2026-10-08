# Raghad-Tamweel-AdvancedMachineLearningMethods-SDA-DSC211

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

Tamweel Lite: Cost-Aware Review Policy for Synthetic Financing Requests

A five-day tabular machine-learning project. It predicts a synthetic default within 90 days of a financing request, validates the model across time and customers, picks a cost-sensitive threshold under a 12% review capacity, checks calibration and explanations, and delivers a reproducible batch policy.

Course: SDA-DSC-211, Advanced Machine Learning Methods. Type: individual project.

Educational use only. All data is synthetic. decision = 1 means refer for review inside a simulation. It is not an approval, a refusal, or a statement about any real person or region.
⸻
Result at a glance
Item	Result
Final model	Logistic Regression (gate decision: KEEP SINGLE)
Mean OOF average precision	0.392 (three forward folds, fold SD 0.030)
Decision rule	flag if calibrated probability >= 0.12226 (raw OOF threshold 0.16892)
OOF at the raw threshold	245 flags of 2,155 (11.4%), recall 46.9%, precision 34.3%, 84 of 179 defaults caught
OOF teaching loss	1,111 units (10 x missed default + 1 x false alarm)
Challenge batch	2,500 requests, 330 above threshold, 300 flagged after the 12% cap
Challenge performance	Not claimed. Challenge labels are unavailable.

Ensemble comparison
⸻
Problem

A review team can examine only a limited share of new requests. Missing a future default costs 10 times a false alarm, and the team can review at most 12% of requests per period.

- Target: default_within_90d, a synthetic event within 90 days after the request.
- Inputs: 22 features available at request time. No identifiers, dates or target in the inputs.
- Challenge set: 2,500 unlabeled requests from customers who do not appear in training.
- Loss: 10 x FN + 1 x FP, in educational units, not real money.
⸻
What each day established
Day	Focus	Main evidence
1	Baseline versus boosting	day1_model_comparison.csv, day1_roc_pr.png
2	Leakage audit, time- and customer-aware validation	leakage_audit.csv, validation_summary.csv
3	Imbalance, threshold sweep, capacity, regional audit	DECISION_CARD.md, threshold_metrics.json
4	SHAP, permutation importance, calibration, stability	INTERPRETABILITY_REPORT.md
5	Worth-it gate, final model, batch policy, delivery	MODEL_CARD.md, ENSEMBLE_DECISION.md, submission.csv
⸻
Key results

Day 1: baseline comparison
Tamweel Lite: Cost-Aware Review Policy for Synthetic Financing Requests

A five-day tabular machine-learning project. It predicts a synthetic default within 90 days of a financing request, validates the model across time and customers, picks a cost-sensitive threshold under a 12% review capacity, checks calibration and explanations, and delivers a reproducible batch policy.

Course: SDA-DSC-211, Advanced Machine Learning Methods. Type: individual project.

Educational use only. All data is synthetic. decision = 1 means refer for review inside a simulation. It is not an approval, a refusal, or a statement about any real person or region.
⸻
Result at a glance
Item	Result
Final model	Logistic Regression (gate decision: KEEP SINGLE)
Mean OOF average precision	0.392 (three forward folds, fold SD 0.030)
Decision rule	flag if calibrated probability >= 0.12226 (raw OOF threshold 0.16892)
OOF at the raw threshold	245 flags of 2,155 (11.4%), recall 46.9%, precision 34.3%, 84 of 179 defaults caught
OOF teaching loss	1,111 units (10 x missed default + 1 x false alarm)
Challenge batch	2,500 requests, 330 above threshold, 300 flagged after the 12% cap
Challenge performance	Not claimed. Challenge labels are unavailable.

Ensemble comparison
⸻
Problem

A review team can examine only a limited share of new requests. Missing a future default costs 10 times a false alarm, and the team can review at most 12% of requests per period.

- Target: default_within_90d, a synthetic event within 90 days after the request.
- Inputs: 22 features available at request time. No identifiers, dates or target in the inputs.
- Challenge set: 2,500 unlabeled requests from customers who do not appear in training.
- Loss: 10 x FN + 1 x FP, in educational units, not real money.
⸻
What each day established
Day	Focus	Main evidence
1	Baseline versus boosting	day1_model_comparison.csv, day1_roc_pr.png
2	Leakage audit, time- and customer-aware validation	leakage_audit.csv, validation_summary.csv
3	Imbalance, threshold sweep, capacity, regional audit	DECISION_CARD.md, threshold_metrics.json
4	SHAP, permutation importance, calibration, stability	INTERPRETABILITY_REPORT.md
5	Worth-it gate, final model, batch policy, delivery	MODEL_CARD.md, ENSEMBLE_DECISION.md, submission.csv
⸻
Key results

Day 1: baseline comparison

On one random stratified split (2,000 comparison rows, about 158 positives), the three models ranked almost the same.
Model	ROC-AUC	AP
Logistic Regression	0.8213	0.016 s
LightGBM	0.8138	0.62 s
XGBoost	0.8124	0.60 s

Gaps near 0.01 on about 158 positives are within likely noise, so boosting showed no clear advantage. The split also shared customers across roles, which Day 2 corrected.

Day 1 ROC and PR

Day 2: honest validation

Two fields (days_past_due_60 and [second field: see leakage_audit.csv]) are recorded after the request, so they were removed. Validation then used forward time folds, separated customers, and a 90-day label-maturity rule.

- AP gap, leaky random minus clean random: 0.6879.
- AP gap, clean random minus honest time-and-customer fixed: -0.0044.
- Only 3 folds, and about 50% of rows (4,961) are warm-up rows with no outer OOF prediction.

Validation comparison

Day 3: threshold under capacity (weighted LightGBM, OOF)
Rule	Loss units	Flag rate	Within 12% in every period
Threshold 0.5	n/a here	19.9%	No
Minimum loss, no capacity limit (0.4486)	2,275	22.6%	No
Minimum loss within capacity (0.6583)	2,639	10.4%	Yes

Respecting capacity costs 364 more loss units than the unconstrained minimum, and recall falls from 0.641 to 0.409 while precision rises from 0.216 to 0.299. Changing the missed-default cost between 8 and 12 did not change the threshold: capacity drives the decision.

Capacity and regions

Day 4: explanation and calibration (weighted LightGBM)

SHAP is in log-odds units. Mean absolute SHAP ranks bureau_score first (0.904), dti second (0.544) and loan_amount_sar third (0.349); permutation importance agrees on the top two. On two separate evaluation periods the sigmoid improved probabilities without changing ranking:
Period	Rows / positives	Brier	ECE
2024Q3	836 / 78	0.1153 to 0.0776	0.1340 to 0.0323
2024Q4	897 / 61	0.1109 to 0.0573	0.1589 to 0.0243

Adding a near-threshold review zone exceeded capacity in both periods (status CAPACITY_REVIEW_REQUIRED), so the threshold was not retuned on evaluation data. These explanations belong to the Day 4 model, not to the final Logistic Regression.

Day 5: worth-it gate

Three single models and three ensembles were compared on nested forward OOF predictions (2,155 rows; folds 2023Q1, 2023Q3, 2024Q1).
Candidate	Mean AP	Fold SD	Brier	ECE	Passes gate
Logistic	0.392	0.030	0.0633	0.0188	reference
Weighted	0.389	0.029	0.0633	0.0177	No
Stack	0.383	0.029	0.0660	0.0311	No
Equal	0.372	0.033	0.0644	0.0204	No
XGBoost	0.353	0.029	0.0657	0.0228	No
LightGBM	0.345	0.043	0.0661	0.0231	No

The closest ensemble trails Logistic by 0.002, far below the fold SD, so no ensemble earned its extra complexity. Decision: KEEP SINGLE.

Calibration of the final model. A sigmoid was fitted on a reserved set (836 rows, 78 positives). It did not help on those rows: Brier 0.0765 to 0.0781, ECE 0.0211 to 0.0349, log loss 0.266 to 0.277. AP (0.288) and ROC-AUC (0.789) are unchanged because the mapping preserves order. These are fit diagnostics on the rows that trained the sigmoid, not an independent test.

Calibration fit

Batch policy. The frozen threshold is applied first, then the highest-probability requests are kept up to the 12% cap. Of 2,500 requests, 330 passed the threshold and 300 were flagged; 30 were removed at boundary score 0.1299.

Challenge capacity

Regional OOF audit (descriptive).
Region	Negatives	False-positive rate	Recall
eastern	507	6.3%	45.7%
central	489	8.0%	50.0%
other	494	8.1%	46.9%
western	486	10.3%	44.7%

Each region has only 35 to 49 positives, so part of the gap may be noise. This is not a fairness certificate.
⸻
Limitations

- Evidence comes from out-of-fold predictions on data used throughout the course. It is not an untouched final test.
- The threshold was chosen on the same OOF labels used to report its loss, so 1,111 units is optimistic.
- Fold SD comes from three overlapping folds and is descriptive, not a confidence interval.
- The sigmoid did not improve calibration on the reserved set, so probability values should be monitored.
- The challenge batch was 13.2% above threshold before capping, against 11.4% in OOF, which may indicate score drift or a riskier batch.
- Day 4 explanations do not describe the final model; its coefficients and case-level reasons still need review.
- Never use this model for real lending or conclusions about real people or regions.

Monitoring plan

Track each batch's pre-cap flag rate against 12%, score and input drift, and calibration. When 90-day outcomes mature, recheck AP, Brier and ECE and decide whether to keep the sigmoid. Review regional rates with their denominators. Develop any model or threshold change on new data, never on the batch being judged.
⸻
Repository layout

README.md
reports/          MODEL_CARD.md, ENSEMBLE_DECISION.md, DECISION_CARD.md, INTERPRETABILITY_REPORT.md
submission/       submission.csv (application_id, probability, decision)
notebooks/        executed notebooks 01 to 05
artifacts/        CSV, JSON and figures from every day, final_model/, final_policy.json
evidence/         day1 to day4 evidence bundles, as exported
scripts/          course pipeline, inference and replay scripts
data/             synthetic data and data contract
presentation/     five-slide PDF


Reproduce

Each notebook runs on free Google Colab CPU and keeps its saved outputs. scripts/replay_final.py checks that the saved submission is reproduced exactly from the exported model without retraining, and scripts/rebuild_final.py retrains from the data.

Data

Fully synthetic and created for the course. It contains no real customers and no real regional or demographic statistics. Monetary values are simulated riyals and losses are educational units.
⸻
الملخص التنفيذي

تم اختيار KEEP SINGLE باستخدام Logistic Regression لأن متوسط AP (على ثلاث طيات) بلغ 0.39166 ولم ينجح أي من نماذج التجميع في تجاوز بوابة الجدوى المحددة مسبقًا. تم تثبيت سياسة القرار والمعايرة، وعند تطبيق النموذج على 2,500 طلب تحدٍ تجاوز 330 طلبًا العتبة، ثم خفّض سقف السعة 12% العدد النهائي إلى 300 إشارة مراجعة. النموذج مخصص للتدريب على بيانات اصطناعية ولا يصلح لاتخاذ قرارات تمويل حقيقية.

On one random stratified split (2,000 comparison rows, about 158 positives), the three models ranked almost the same.
Model	ROC-AUC	AP
Logistic Regression	0.8213	0.016 s
LightGBM	0.8138	0.62 s
XGBoost	0.8124	0.60 s

Gaps near 0.01 on about 158 positives are within likely noise, so boosting showed no clear advantage. The split also shared customers across roles, which Day 2 corrected.

Day 1 ROC and PR


Day 2: honest validation

Two fields (days_past_due_60 and [second field: see leakage_audit.csv]) are recorded after the request, so they were removed. Validation then used forward time folds, separated customers, and a 90-day label-maturity rule.

- AP gap, leaky random minus clean random: 0.6879.
- AP gap, clean random minus honest time-and-customer fixed: -0.0044.
- Only 3 folds, and about 50% of rows (4,961) are warm-up rows with no outer OOF prediction.

Validation comparison

Day 3: threshold under capacity (weighted LightGBM, OOF)
Rule	Loss units	Flag rate	Within 12% in every period
Threshold 0.5	n/a here	19.9%	No
Minimum loss, no capacity limit (0.4486)	2,275	22.6%	No
Minimum loss within capacity (0.6583)	2,639	10.4%	Yes

Respecting capacity costs 364 more loss units than the unconstrained minimum, and recall falls from 0.641 to 0.409 while precision rises from 0.216 to 0.299. Changing the missed-default cost between 8 and 12 did not change the threshold: capacity drives the decision.

Capacity and regions

Day 4: explanation and calibration (weighted LightGBM)

SHAP is in log-odds units. Mean absolute SHAP ranks bureau_score first (0.904), dti second (0.544) and loan_amount_sar third (0.349); permutation importance agrees on the top two. On two separate evaluation periods the sigmoid improved probabilities without changing ranking:
Period	Rows / positives	Brier	ECE
2024Q3	836 / 78	0.1153 to 0.0776	0.1340 to 0.0323
2024Q4	897 / 61	0.1109 to 0.0573	0.1589 to 0.0243

Adding a near-threshold review zone exceeded capacity in both periods (status CAPACITY_REVIEW_REQUIRED), so the threshold was not retuned on evaluation data. These explanations belong to the Day 4 model, not to the final Logistic Regression.

Day 5: worth-it gate

Three single models and three ensembles were compared on nested forward OOF predictions (2,155 rows; folds 2023Q1, 2023Q3, 2024Q1).
Candidate	Mean AP	Fold SD	Brier	ECE	Passes gate
Logistic	0.392	0.030	0.0633	0.0188	reference
Weighted	0.389	0.029	0.0633	0.0177	No
Stack	0.383	0.029	0.0660	0.0311	No
Equal	0.372	0.033	0.0644	0.0204	No
XGBoost	0.353	0.029	0.0657	0.0228	No
LightGBM	0.345	0.043	0.0661	0.0231	No

The closest ensemble trails Logistic by 0.002, far below the fold SD, so no ensemble earned its extra complexity. Decision: KEEP SINGLE.

Calibration of the final model. A sigmoid was fitted on a reserved set (836 rows, 78 positives). It did not help on those rows: Brier 0.0765 to 0.0781, ECE 0.0211 to 0.0349, log loss 0.266 to 0.277. AP (0.288) and ROC-AUC (0.789) are unchanged because the mapping preserves order. These are fit diagnostics on the rows that trained the sigmoid, not an independent test.

Calibration fit

Batch policy. The frozen threshold is applied first, then the highest-probability requests are kept up to the 12% cap. Of 2,500 requests, 330 passed the threshold and 300 were flagged; 30 were removed at boundary score 0.1299.

Challenge capacity

Regional OOF audit (descriptive).
Region	Negatives	False-positive rate	Recall
eastern	507	6.3%	45.7%
central	489	8.0%	50.0%
other	494	8.1%	46.9%
western	486	10.3%	44.7%

Each region has only 35 to 49 positives, so part of the gap may be noise. This is not a fairness certificate.
⸻
Limitations

- Evidence comes from out-of-fold predictions on data used throughout the course. It is not an untouched final test.
- The threshold was chosen on the same OOF labels used to report its loss, so 1,111 units is optimistic.
- Fold SD comes from three overlapping folds and is descriptive, not a confidence interval.
- The sigmoid did not improve calibration on the reserved set, so probability values should be monitored.
- The challenge batch was 13.2% above threshold before capping, against 11.4% in OOF, which may indicate score drift or a riskier batch.
- Day 4 explanations do not describe the final model; its coefficients and case-level reasons still need review.
- Never use this model for real lending or conclusions about real people or regions.

Monitoring plan

Track each batch's pre-cap flag rate against 12%, score and input drift, and calibration. When 90-day outcomes mature, recheck AP, Brier and ECE and decide whether to keep the sigmoid. Review regional rates with their denominators. Develop any model or threshold change on new data, never on the batch being judged.
⸻
Repository layout

README.md
reports/          MODEL_CARD.md, ENSEMBLE_DECISION.md, DECISION_CARD.md, INTERPRETABILITY_REPORT.md
submission/       submission.csv (application_id, probability, decision)
notebooks/        executed notebooks 01 to 05
artifacts/        CSV, JSON and figures from every day, final_model/, final_policy.json
evidence/         day1 to day4 evidence bundles, as exported
scripts/          course pipeline, inference and replay scripts
data/             synthetic data and data contract
presentation/     five-slide PDF


Reproduce

Each notebook runs on free Google Colab CPU and keeps its saved outputs. scripts/replay_final.py checks that the saved submission is reproduced exactly from the exported model without retraining, and scripts/rebuild_final.py retrains from the data.
##Data

Fully synthetic and created for the course. It contains no real customers and no real regional or demographic statistics. Monetary values are simulated riyals and losses are educational units.
⸻
الملخص التنفيذي

تم اختيار KEEP SINGLE باستخدام Logistic Regression لأن متوسط AP (على ثلاث طيات) بلغ 0.39166 ولم ينجح أي من نماذج التجميع في تجاوز بوابة الجدوى المحددة مسبقًا. تم تثبيت سياسة القرار والمعايرة، وعند تطبيق النموذج على 2,500 طلب تحدٍ تجاوز 330 طلبًا العتبة، ثم خفّض سقف السعة 12% العدد النهائي إلى 300 إشارة مراجعة. النموذج مخصص للتدريب على بيانات اصطناعية ولا يصلح لاتخاذ قرارات تمويل حقيقية.
