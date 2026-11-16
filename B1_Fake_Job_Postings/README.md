# B1 — Detecting Fraudulent Job Postings

Supervised binary classification on the EMSCAD corpus (`shivamb/real-or-fake-fake-jobposting-prediction`, CC0).
The positive class is `fraudulent = 1`; the dataset is severely imbalanced (866 of 17,880 postings, 4.84 %).

**Notebook:** `B1_notebook.ipynb` (executed, no errors)
**Report:** `report/70173809_B1_Report.pdf`
**Seed:** 42 (split, CV folds, every model)

## How to run

1. Download the data into `data/` as described in `data/README.md`.
2. From this folder: `jupyter notebook B1_notebook.ipynb` → Restart & Run All.

The notebook rewrites `figures/` and `results/`.

## Method

- 70 / 15 / 15 stratified split → 12,516 train, 2,682 validation, 2,682 test postings.
- `ColumnTransformer`: median-impute + scale the 7 numeric features, pass the 3 binary
  flags, one-hot the 6 categoricals (rare levels grouped), and TF-IDF the concatenated
  text (word 1–2-grams, 20,000 features, `min_df=3`, sublinear TF).
- The representation is fitted once on the training split only.
- Logistic Regression and a Linear SVM are tuned with 3-fold CV PR-AUC; LightGBM uses a
  fixed 150-tree sparse configuration (and is compared through the validation split).
- Each model's threshold is chosen on validation to maximise fraud F1; the test split is
  evaluated once. Class weighting is ablated.

## Results (test set, n = 2,682; 130 fraudulent)

| Model | Threshold | Precision | Recall | F1 | PR-AUC | ROC-AUC |
|---|---|---|---|---|---|---|
| Logistic Regression | 0.7529 | 0.8106 | 0.8231 | 0.8168 | 0.9027 | 0.9908 |
| Linear SVM | 0.4173 | 0.8947 | 0.7846 | 0.8361 | 0.9178 | 0.9912 |
| LightGBM | 0.5286 | 0.8938 | 0.7769 | 0.8313 | 0.9191 | 0.9921 |

Always-"real" accuracy is 0.9515 and catches 0 frauds; the best model trades about 3.3
accuracy points for an F1 of 0.83.

Ablation (LightGBM, test): structured-only 0.7947 PR-AUC / 0.6983 F1; text-only 0.8898 /
0.8374; combined 0.9191 / 0.8313. Text carries most of the signal; metadata adds +0.029
PR-AUC but does not move F1. Balancing the classes raises validation PR-AUC from 0.8786
to 0.9199 and validation F1 from 0.8085 to 0.8482.

## Artifacts

- `figures/` — missingness, class balance, fraud-rate EDA, PR curves, confusion matrix,
  ablation bars, top TF-IDF coefficients.
- `results/` — split, CV, validation, test, class-weight check, ablation, top features,
  false positives and a machine-readable `b1_summary.json`.
