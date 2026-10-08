






# Tamweel Lite — Cost-Aware Credit-Risk Review Policy

An end-to-end tabular machine-learning project that predicts a **synthetic financing default within 90 days of application**. The project focuses on honest validation across time and customers, cost-sensitive decision-making under a **12% review capacity**, calibration, interpretability, and a reproducible final batch policy.

**Course:** SDA-DSC-211 — Advanced Machine Learning Methods (SDAIA Academy) **Project Type:** Individual Five-Day Project **Session:** October 2026

> **Educational use only.** All data is fully synthetic. A `decision = 1` means _refer for review_ within a simulation. It is not an approval, a refusal, or a statement about any real person or region.

---

## Final Decision at a Glance

| Item | Result |
| --- | --- |
| Final model | **\[MODEL NAME\]** |
| Mean OOF Average Precision | **\[AP\]** |
| OOF fold SD | **\[SD\]** |
| Decision threshold | **\[THRESHOLD\]** |
| OOF recall | **\[RECALL\]%** |
| OOF precision | **\[PRECISION\]%** |
| Review capacity | **\[FLAG RATE\]%** |
| Decision loss | **\[LOSS\] units** |
| Challenge batch | **\[N\] applications** |
| Applications flagged | **\[N\]** |
| Challenge performance | **Not claimed — challenge labels are unavailable** |

> Final values will be populated only from the executed project outputs. No metrics are manually entered or fabricated.

---

## The Problem

A lender has a limited review team and must decide which new applications should be referred for additional review.

The educational policy assigns:

- **10× cost** to a false negative (`FN`)
- **1× cost** to a false positive (`FP`)
- A maximum review capacity of **12% per validation period**

The goal is therefore not simply to maximize accuracy. The project aims to identify a model and decision threshold that provide useful ranking performance while respecting the operational review constraint.

### Target

`default_within_90d = 1`

The target represents a **synthetic financing default occurring within 90 days after application**.

It does not mean that the application was 90 days past due.

---

## Project Objectives

The project is designed to:

1. Build a reliable tabular classification pipeline.
2. Prevent temporal and customer-level leakage.
3. Compare baseline and machine-learning models fairly.
4. Validate using honest time- and customer-aware splits.
5. Select a decision threshold using OOF predictions.
6. Apply the `10 × FN + 1 × FP` educational cost policy.
7. Respect the **12% review-capacity constraint**.
8. Evaluate probability calibration using Brier score, ECE, and reliability curves.
9. Interpret the final model using appropriate explanation methods.
10. Evaluate whether an ensemble provides stable additional value.
11. Produce a reproducible inference pipeline and final batch policy.

---

## Five-Day Build

| Day | Focus | Main Evidence |
| --- | --- | --- |
| **1** | Baseline and model comparison | `day1_model_comparison.csv`, ROC/PR curves |
| **2** | Leakage audit and honest validation | `leakage_audit.csv`, `fold_audit.csv`, `validation_summary.csv` |
| **3** | Cost-sensitive threshold and capacity policy | `DECISION_CARD.md`, `threshold_metrics.json` |
| **4** | Interpretability, calibration and stability | `INTERPRETABILITY_REPORT.md` |
| **5** | Ensemble gate, final model and delivery | `ENSEMBLE_DECISION.md`, `MODEL_CARD.md`, `submission.csv` |

---

# Day 1 — Baseline and Model Comparison

The first stage establishes a fair comparison between the selected candidate models using the same comparison data and preprocessing logic.

### Models

- Logistic Regression
- XGBoost
- LightGBM

### Results

| Model | ROC-AUC | Average Precision | Train Time |
| --- | --- | --- | --- |
| Logistic Regression | `[ 0.8213]` | `[0.3258 ]` | `[ 0.0645]` |
| XGBoost | `[0.8214 ]` | `[0.3338 ]` | `[ 0.4209]` |
| LightGBM | `[ 0.8138]` | `[ 0.3248]` | `[ 0.3309]` |

### Interpretation

The Day 1 comparison identifies the initial candidate model based on ranking performance, computational cost, and practical simplicity.

**Selected candidate:** `[MODEL]`

!Day 1 ROC and PR curves

---

# Day 2 — Honest Validation and Leakage Control

A major objective of the project is to avoid overly optimistic validation.

The validation design separates observations across:

- **Time**
- **Customers**
- **Target maturity**

All preprocessing operations, including imputation and weighting, are fitted using training rows only.

### Leakage Audit

Potential post-decision variables are explicitly reviewed before modelling.

<img width="953" height="386" alt="‏لقطة الشاشة ١٤٤٨-٠٤-٢٧ في ٣ ٥٩ ٤٣ م" src="https://github.com/user-attachments/assets/d6de7545-3111-477b-8434-8a9db72fb6b9" />




The final validation scheme is selected based on temporal realism, customer separation, target maturity, and leakage prevention.

!Validation comparison

---

# Day 3 — Cost-Sensitive Threshold Under 12% Capacity

The model probability is converted into a review decision using a threshold selected from **OOF predictions**.

The educational loss function is:

```
Loss = 10 × FN + 1 × FP
```

The review capacity must remain:

```
Review rate ≤ 12%
```

### Threshold Comparison

<img width="1044" height="295" alt="‏لقطة الشاشة ١٤٤٨-٠٤-٢٧ في ٤ ٣٢ ٤٦ م" src="https://github.com/user-attachments/assets/f00b0807-22ec-4161-9cf2-8ce4faea999d" />




<img width="957" height="361" alt="‏لقطة الشاشة ١٤٤٨-٠٤-٢٧ في ٤ ١٦ ٥٢ م" src="https://github.com/user-attachments/assets/207474d0-6183-4aa8-af67-011fdf58f449" />



The selected threshold is the **minimum-loss feasible threshold under the 12% capacity constraint**, based on the prescribed OOF procedure.

!Capacity and threshold analysis

---

# Day 4 — Interpretability and Calibration

## Interpretability

The project uses model-appropriate explanation methods to understand how features influence predictions.

Where applicable:

- SHAP
- Permutation importance
- Feature contribution analysis

SHAP explanations describe the behavior of the fitted model. They **do not establish causality, fairness, or legal compliance**.

!Feature importance

## Calibration

Probability quality is evaluated separately from ranking quality.

The project reports:

- Brier Score
- Expected Calibration Error (ECE)
- Reliability Curve
- Log-loss

### Calibration Results

| Metric | Raw | Calibrated |
| --- | --- | --- |
| Brier | `[ ]` | `[ ]` |
| ECE | `[ ]` | `[ ]` |
| Log-loss | `[ ]` | `[ ]` |
| ROC-AUC | `[ ]` | `[ ]` |
| Average Precision | `[ ]` | `[ ]` |

Calibration is learned using calibration rows only and frozen before policy or evaluation use.

!Calibration curve

---

# Day 5 — Ensemble Worth-It Gate

The final model is selected using a documented **Worth-It Gate**.

An ensemble is considered only if it provides stable improvement over the best single model without unacceptable deterioration in calibration or other required metrics.

### Model Comparison



<img width="973" height="611" alt="‏لقطة الشاشة ١٤٤٨-٠٤-٢٧ في ٤ ٢٢ ٥٤ م" src="https://github.com/user-attachments/assets/82db2f8c-08c5-4ed5-aafe-2dda3383fac0" />





### Final Decision

**`[KEEP_SINGLE_MODEL / SHIP_ENSEMBLE]`**

The final choice is based on measured evidence rather than model complexity alone.

!Ensemble comparison

---

# Final Batch Policy

The final policy follows a fixed sequence:

```
New application
       ↓
Feature preprocessing
       ↓
Final model
       ↓
Probability
       ↓
Frozen threshold
       ↓
Review decision
       ↓
12% capacity check
       ↓
Final batch output
```

If more than 12% of applications pass the threshold, the policy applies the documented capacity rule and retains the highest-priority applications according to the frozen policy.

### Final Output

The inference interface returns:

```
application_id
probability
decision
```

The final submission is stored in:

```
submission.csv
```

---

# Regional Audit

Regional results are reported descriptively and are not interpreted as a fairness certificate.

| Region | Flag Rate | False Positive Rate | Recall | N |
| --- | --- | --- | --- | --- |
| Eastern | `[ ]` | `[ ]` | `[ ]` | `[ ]` |
| Central | `[ ]` | `[ ]` | `[ ]` | `[ ]` |
| Western | `[ ]` | `[ ]` | `[ ]` | `[ ]` |
| Other | `[ ]` | `[ ]` | `[ ]` | `[ ]` |

Small subgroup counts may produce unstable estimates. Any notable differences are treated as monitoring signals requiring further investigation.

---

# Limitations

- The data is fully synthetic and does not represent real customers.
- Challenge labels are unavailable; therefore, challenge performance is **not claimed**.
- OOF results are development evidence and are not equivalent to an untouched final test set.
- Threshold selection can introduce optimism when the same OOF predictions are used for reporting.
- Fold-level variation is descriptive and should not automatically be interpreted as a confidence interval.
- Calibration may not improve probability quality and should therefore be monitored.
- Regional metrics are descriptive and do not constitute a fairness certification.
- Model explanations describe model behavior and do not establish causality.
- The system is designed for educational purposes and must not be used for real financing decisions.

---

# Monitoring Plan

After deployment-style simulation, monitor:

- Pre-cap review rate against the **12% limit**.
- Probability and score distributions.
- Observed target prevalence after outcomes mature.
- Average Precision.
- Brier Score.
- ECE.
- Calibration stability.
- Regional false-positive rate and recall.
- Changes in data and feature distributions.

Any model or threshold change must be developed and validated using new eligible data rather than the batch being evaluated.

---

# Repository Structure

```
├── README.md
├── ADMINISTRATIVE_REQUIREMENTS.md
├── TECHNICAL_REQUIREMENTS.md
│
├── MODEL_CARD.md
├── DECISION_CARD.md
├── INTERPRETABILITY_REPORT.md
├── ENSEMBLE_DECISION.md
│
├── submission.csv
├── metrics.json
│
├── notebooks/
│   ├── 00_environment_and_data.ipynb
│   ├── 01_day1_model_comparison.ipynb
│   ├── 02_day2_validation.ipynb
│   ├── 03_day3_threshold_policy.ipynb
│   ├── 04_day4_interpretability.ipynb
│   ├── 05_day5_final_model.ipynb
│   └── 99_final_check.ipynb
│
├── artifacts/
│   ├── day1/
│   ├── day2/
│   ├── day3/
│   ├── day4/
│   ├── day5/
│   ├── final_model/
│   └── final_policy.json
│
├── evidence/
│   ├── day1/
│   ├── day2/
│   ├── day3/
│   └── day4/
│
├── reports/
├── submission/
├── tamweel/
├── scripts/
├── data/
├── presentation/
│   └── final_presentation.pdf
│
├── requirements-colab.txt
├── constraints.txt
└── environment.json
```

---

# Reproducibility

The project is designed to run on **free Google Colab CPU** without:

- Paid services
- API keys
- GPU
- Required Google Drive mounting
- Local installation dependencies

The project records:

- Random seeds
- Package versions
- Model parameters
- Data hashes
- Provenance
- Generated artifacts
- Repository commit SHA

### Replay

```
pip install -r requirements-colab.txt -c constraints.txt

cd scripts

python replay_final.py
```

Expected successful output:

```
REPLAY_MATCH
```

A full rebuild can be executed using:

```
python rebuild_final.py
```

The final repository must reproduce the submitted probabilities and outputs from the recorded source version.

---

# Data

All Tamweel Lite data is **synthetic course data**.

It contains:

- No real customers
- No real financing records
- No real regional statistics
- No real demographic information

The challenge labels remain unavailable to the learner workflow.

All monetary values and decision losses are simulated for educational purposes.

---

# Required Project Evidence

The final repository contains the following key evidence:

| Evidence | File |
| --- | --- |
| Decision policy | `DECISION_CARD.md` |
| Model explanation | `INTERPRETABILITY_REPORT.md` |
| Ensemble decision | `ENSEMBLE_DECISION.md` |
| Final model documentation | `MODEL_CARD.md` |
| Final predictions | `submission.csv` |
| Final metrics | `metrics.json` |
| Frozen policy | `artifacts/final_policy.json` |
| Final model | `artifacts/final_model/` |
| Reproducibility | `environment.json` \+ manifest |
| Final presentation | `presentation/final_presentation.pdf` |

---

# Administrative Compliance

This repository follows the SDA-DSC-211 administrative requirements, including:

- Official student repository structure.
- Professional README documentation.
- Technical documentation and provenance.
- Meaningful Git history.
- Required project reports.
- Five-slide final presentation.
- Final commit and tag.
- Exact commit SHA recording.
- Reproducible final bundle.
- Appropriate disclosure of sources and assistance.
- No private personal information or challenge labels.

The administrative requirements define the repository, documentation, submission, version-control, reporting, presentation, and defence expectations.  GitHub

---

# Technical Compliance

The project follows the required technical contract:

- Free Google Colab CPU environment.
- Synthetic course data only.
- Training-only preprocessing.
- Honest OOF predictions.
- `10 × FN + 1 × FP` decision loss.
- Maximum **12% review capacity**.
- Model-appropriate interpretability.
- Calibration learned on calibration data only.
- Documented ensemble Worth-It Gate.
- Reproducible inference interface.
- Recorded seeds, versions, hashes and provenance.
- No fabricated metrics, outputs, commits or timestamps.

These requirements are defined in the official technical requirements for the project.  GitHub

---

# Executive Summary

## English

Tamweel Lite is an end-to-end educational machine-learning project for predicting synthetic financing defaults within 90 days of application. The project emphasizes honest validation across time and customers, leakage prevention, cost-sensitive threshold selection, a 12% review-capacity constraint, calibration, interpretability, and reproducible batch inference.

The final model, threshold, calibration approach, and ensemble decision will be selected strictly from executed project evidence and documented in the final repository.

## الملخص التنفيذي

**Tamweel Lite** هو مشروع متكامل في تعلم الآلة يهدف إلى التنبؤ بالتعثر التمويلي الاصطناعي خلال 90 يومًا من تاريخ التقديم.

يركز المشروع على:

- التحقق الزمني وعلى مستوى العملاء.
- منع تسرب البيانات.
- اختيار عتبة قرار تراعي التكلفة.
- الالتزام بسعة مراجعة لا تتجاوز **12%**.
- تقييم معايرة الاحتمالات.
- تفسير النموذج.
- بناء سياسة نهائية قابلة لإعادة الإنتاج.

سيتم اختيار النموذج والعتبة وسياسة المعايرة وقرار استخدام التجميع بناءً على النتائج الفعلية الناتجة من تنفيذ المشروع، وليس على نتائج مفترضة.

---

# Educational Disclaimer

> This project is for educational purposes only. All data is synthetic. The model and decision policy are part of a course simulation and must not be used to make real financing, credit, regional, demographic, or individual-level decisions.

---

# Training Programme

This project is completed as part of:

**SDA-DSC-211 — Advanced Machine Learning Methods**

**Provider:** SDAIA Academy via Learning Space **Project Type:** Individual Five-Day Project **Session:** October 2026

Training-program reference: [SDAIA Academy on GitHub](<https://github.com/SDAIAAcademy?utm_source=chatgpt.com>)
.
