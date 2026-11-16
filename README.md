# AI101-ML-Assignment-70173809

**Student:** Manaal Pervaiz
**Roll No.:** 70173809
**Section:** BSES A
**Course:** AI-101 Introduction to Artificial Intelligence (Fall 2026)
**Instructor:** Dr. Muhammad Awais, AI Architect, Department of Intelligent Systems, The University of Lahore

## Graded tasks (one per pool)

| Pool | Task ID | Task | Notebook | Report |
|---|---|---|---|---|
| A — Numerical | **A1** | Breast Cancer Diagnosis from Cell-Nucleus Measurements | [A1_notebook.ipynb](A1_Breast_Cancer/A1_notebook.ipynb) | [70173809_A1_Report.pdf](A1_Breast_Cancer/report/70173809_A1_Report.pdf) |
| B — Mixed (numerical + text) | **B1** | Detecting Fraudulent Job Postings | [B1_notebook.ipynb](B1_Fake_Job_Postings/B1_notebook.ipynb) | [70173809_B1_Report.pdf](B1_Fake_Job_Postings/report/70173809_B1_Report.pdf) |
| C — Sequence-to-sequence | **C3** | Image Captioning with a CNN Encoder and an LSTM Decoder | [C3_notebook.ipynb](C3_Image_Captioning/C3_notebook.ipynb) | [70173809_C3_Report.pdf](C3_Image_Captioning/report/70173809_C3_Report.pdf) |

Bonus tasks: **none** — three graded tasks only.

## Repository layout

```text
AI101-ML-Assignment-70173809/
|-- README.md
|-- AI_DISCLOSURE.md
|-- requirements.txt
|-- .gitignore
|-- A1_Breast_Cancer/
|   |-- A1_notebook.ipynb          executed notebook with all outputs
|   |-- figures/                   EDA and result figures used in the report
|   |-- results/                   metric tables saved by the notebook
|   |-- report/
|   |   |-- 70173809_A1_Report.pdf
|   |   `-- 70173809_A1_Report.tex  LaTeX source
|   `-- data/README.md             data source notes (sklearn built-in)
|-- B1_Fake_Job_Postings/          same layout
`-- C3_Image_Captioning/           same layout
```

## How to run

Pool A and Pool B run locally on CPU with Python 3.11:

```bash
python -m venv .venv
.venv\Scripts\activate            # Windows
pip install -r requirements.txt
jupyter notebook
```

Then open the task notebook and **Run All**. Each notebook is self-contained,
fixes the random seed, and writes its figures to `figures/` and its metric
tables to `results/`.

Pool C (C3) trains on a GPU. Upload/push `C3_Image_Captioning/C3_notebook.ipynb`
to a Kaggle Notebook with a T4 GPU, Internet enabled, and the
`adityajn105/flickr8k` dataset attached via **Add Input**, then Run All. The
executed notebook is downloaded and committed here. The report states the
platform, GPU and training time.

## Reproducibility

- Random seed: **42** (NumPy, scikit-learn, PyTorch, Python `random`).
- Versions are pinned in `requirements.txt`.
- All preprocessing (scalers, vectorisers, imputers) is fitted on the training
  split only; the test split is used once, for final evaluation.
- Every number reported in the PDF reports is produced by the corresponding
  notebook and stored in its `results/` folder.

## AI use

See [AI_DISCLOSURE.md](AI_DISCLOSURE.md). A per-task statement also appears at
the end of each report.
