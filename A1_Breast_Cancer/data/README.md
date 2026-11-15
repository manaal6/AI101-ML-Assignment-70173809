# A1 — Data source

**Dataset:** Breast Cancer Wisconsin (Diagnostic)
**Source:** UCI Machine Learning Repository, dataset id 17
**Loader used in the notebook:** `sklearn.datasets.load_breast_cancer(as_frame=True)`

This dataset ships with scikit-learn, so **no download is required**. The notebook
loads the 569 x 30 matrix directly and does not read any local CSV.

## Provenance
The features are computed from a digitised image of a fine-needle aspirate (FNA)
of a breast mass. For each of ten nucleus properties (radius, texture, perimeter,
area, smoothness, compactness, concavity, concave points, symmetry, fractal
dimension) the mean, standard error and "worst" value are recorded, giving 30
real-valued features.

## Class encoding in the notebook
`load_breast_cancer` encodes the target as `0 = malignant`, `1 = benign`.
Because the task asks for **malignant as the positive class**, the notebook
re-encodes the target as:

```python
y = (data.target == 0).astype(int)   # 1 = malignant (212), 0 = benign (357)
```

## Optional raw download
The same data can be obtained from UCI:

```bash
curl -O https://archive.ics.uci.edu/static/public/17/breast+cancer+wisconsin+diagnostic.zip
```

## Citation
W. N. Street, W. H. Wolberg and O. L. Mangasarian, "Nuclear feature extraction
for breast tumor diagnosis," *Proc. IS&T/SPIE 1993 International Symposium on
Electronic Imaging*, vol. 1905, pp. 861-870, 1993.
