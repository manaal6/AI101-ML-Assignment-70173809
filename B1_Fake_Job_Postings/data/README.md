# B1 — Data source

**Dataset:** Real or Fake Job Posting Prediction (EMSCAD)
**Source:** Kaggle, `shivamb/real-or-fake-fake-jobposting-prediction`
**File used:** `fake_job_postings.csv` (17,880 rows x 18 columns, 866 fraudulent)

Datasets are not committed to this repository (course rule, and the file is
larger than necessary for git). Download it with the Kaggle CLI:

```bash
pip install kaggle
# put your API token at ~/.kaggle/kaggle.json (or %USERPROFILE%\.kaggle\kaggle.json)
kaggle datasets download -d shivamb/real-or-fake-fake-jobposting-prediction --unzip -p data/
```

Expected layout after download:

```text
B1_Fake_Job_Postings/
  data/
    fake_job_postings.csv
```

The notebook reads `data/fake_job_postings.csv` and fails with a clear message
if the file is absent.

## Columns
- Identifier / administrative: `job_id`
- Target: `fraudulent` (0 = real, 1 = fraudulent)
- Binary flags: `telecommuting`, `has_company_logo`, `has_questions`
- Categorical: `employment_type`, `required_experience`, `required_education`,
  `industry`, `function`, `location`, `country`, `department`
- Free text: `title`, `company_profile`, `description`, `requirements`, `benefits`

## Notes on the data
- `company_profile` is missing for a large share of fraudulent postings, so
  missingness itself is a signal. The notebook adds explicit missing flags.
- The dataset is severely imbalanced (about 4.8 % fraudulent), so accuracy is
  misleading and F1 / PR-AUC are the primary metrics.

## Citation
S. Bhardwaj, "Real or Fake Job Posting Prediction," Kaggle, 2020.
https://www.kaggle.com/datasets/shivamb/real-or-fake-fake-jobposting-prediction

Underlying corpus: EMSCAD (Employment Scam Aegean Dataset), University of the
Aegean, Laboratory of Information and Communication Systems Security.
