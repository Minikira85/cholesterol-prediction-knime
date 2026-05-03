# Predicting Total Cholesterol from Clinical Lab Data - KNIME Regression Workflow

Can glucose, age, and sex predict total cholesterol in an ambulatory population? This project builds and evaluates a linear regression model in KNIME using real clinical laboratory data to answer that question and finds that the answer, while statistically modest, is clinically informative.

**Context:** Microcredential in AI & Big Data in Health UAB / Hospital Parc Taulí, 2026

---

## The clinical question

Glucose and total cholesterol are both implicated in metabolic syndrome, where they often appear altered together. The hypothesis was that glucose level, combined with age and sex, could serve as a predictor of total cholesterol in routine ambulatory patients.

---

## Dataset

933 ambulatory patients with simultaneous glucose and total cholesterol determinations from a real clinical laboratory setting (October–December 2025). Variables used: total cholesterol (target), blood glucose, age, and sex.

Patient identifiers and personal data have been fully removed from all outputs. The raw dataset is not included in this repository for patient confidentiality reasons.

---

## Workflow

The KNIME workflow consists of 6 nodes:

| Node | Purpose |
|---|---|
| CSV Reader | Loads 933 patient records (19 columns) |
| Column Filter | Selects the 4 relevant variables, removes identifiers and duplicates from dataset merge |
| Linear Correlation | Computes pairwise correlations between numeric variables |
| Table Partitioner | 70/30 train/test split, stratified by sex, fixed random seed for reproducibility |
| Linear Regression Learner | Trains the model on the training partition |
| Numeric Scorer | Evaluates predictions against ground truth (R², MAE, RMSE, MSE, adjusted R²) |

Workflow screenshots are included in the `workflow_screenshots/` folder.

---

## Results

| Metric | Value |
|---|---|
| R² | 0.024 |
| Adjusted R² | 0.024 |
| RMSE | 42.98 mg/dL |
| MAE | 33.45 mg/dL |

Correlation analysis: glucose and total cholesterol showed a weak negative correlation (r = −0.095, p = 0.004). Age correlated moderately with glucose (r = 0.249) but minimally with cholesterol (r = 0.043).

---

## Clinical interpretation

The low R² is not a modelling failure — it is a clinically coherent result. Total cholesterol in an ambulatory population under active follow-up is strongly influenced by factors not captured in this dataset: dietary habits, physical activity, statin therapy, and thyroid function. In a population that has already been identified and treated, glucose is not expected to be a strong predictor of cholesterol. The combination of correlation analysis and regression modelling makes this conclusion rigorous and reproducible, which has value in applied health science independent of the metric value.

---

## Stack

`KNIME Analytics Platform` · `Linear Regression` · `Linear Correlation` · `CSV` · `Clinical laboratory data`

---

## Next steps

Comparing performance against non-linear models (Random Forest, k-NN regression) would allow a more complete evaluation of whether the low variance explained reflects a genuine absence of linear relationship or a limitation of the model family.
