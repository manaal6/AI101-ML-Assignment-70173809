# A1 — Breast Cancer Diagnosis from Cell-Nucleus Measurements

Supervised binary classification on the UCI Breast Cancer Wisconsin (Diagnostic)
dataset. The positive class is **malignant** (originally `target = 0`, re-encoded
to 1); 212 of 569 samples are malignant (37.3%).

**Notebook:** `A1_notebook.ipynb` (executed, no errors)
**Report:** `report/70173809_A1_Report.pdf`
**Seed:** 42 (split, CV folds, every model)

## How to run

The dataset ships with scikit-learn, so no download is needed.

```bash
jupyter notebook A1_notebook.ipynb    # Restart & Run All
```

The notebook rewrites `figures/` and `results/`.

## Method

- Stratified 80 / 20 split: 455 train, 114 test (42 malignant).
- 5-fold stratified CV on the training split; scaler fitted inside each fold.
- Logistic Regression, RBF-kernel SVM and Random Forest tuned by grid search on
  CV F1; the test split is evaluated once.
- Default threshold 0.5, then a threshold chosen on out-of-fold predictions to
  target recall 0.97.
- Ablation drops 7 of 30 features from two correlation groups (15 pairs with
  |r| >= 0.95).

## Results (test set, n = 114)

| Model | Threshold | Accuracy | Precision | Recall | F1 | ROC-AUC |
|---|---|---|---|---|---|---|
| Logistic Regression | 0.50 | 0.9649 | 0.9750 | 0.9286 | 0.9512 | 0.9960 |
| SVM (RBF) | 0.50 | 0.9737 | 1.0000 | 0.9286 | 0.9630 | 0.9927 |
| Random Forest | 0.50 | 0.9649 | 1.0000 | 0.9048 | 0.9500 | 0.9942 |

CV F1: LR 0.9640 +/- 0.0207, SVM 0.9674 +/- 0.0114, RF 0.9489 +/- 0.0210.
Best model: SVM (C = 10, gamma = scale).

Threshold study (SVM): t = 0.38 gives recall 0.952 (40/42), precision 0.976,
F1 0.9639, one false positive and two false negatives (precision cost 0.024).
A constant benign predictor scores 0.6316.

Ablation: dropping 7 correlated features leaves 23 and changes nothing for the
SVM (F1 0.963, ROC-AUC +0.0007); Random Forest loses 0.0133 F1.

## Artifacts

- `figures/` — class balance, correlation heatmaps, ROC curves, confusion
  matrices, threshold sweep, importances and coefficients.
- `results/` — dataset summary, CV results, grid-search parameters, test
  metrics, threshold study, correlation groups, ablation and
  `a1_summary.json`.
