# AI Use Disclosure

This file records how generative AI tools were used in this assignment, as
required by Section 7 of the AI-101 assignment brief. The same statement, in
task-specific form, appears at the end of each report.

## Tool used

**opencode** (terminal coding assistant, model `deepseek-v4.1-flash-free`),
used interactively during October–November 2026.

## Purpose of use

The tool was used for the following permitted purposes:

1. **Concept explanation and debugging** — explaining scikit-learn pipeline
   behaviour, `ColumnTransformer` wiring, class-imbalance handling, sequence
   decoding and BLEU computation, and diagnosing execution errors.
2. **Boilerplate and scaffolding** — drafting notebook scaffolding (imports,
   plotting helpers, table formatting) and report LaTeX structure, which were
   then read, run and corrected.
3. **Hyperparameter ranges** — suggesting candidate grids to try (for example
   `C` and `gamma` for the RBF SVM). The final grids, runs and selected values
   were executed and checked by the student.
4. **Wording** — improving the grammar and clarity of text written by the
   student.

## Parts generated or substantially assisted by AI

| Task | Assisted parts |
|---|---|
| A1 | Notebook scaffolding; EDA plotting code; threshold-sweep helper; first draft of report sections 1–7 |
| B1 | Notebook scaffolding; `ColumnTransformer` template; ablation table code; first draft of report sections 1–7 |
| C3 | Notebook scaffolding; feature-caching code; beam-search helper; first draft of report sections 1–7 |
| All | This disclosure file |

## How the content was verified

- Every notebook was executed from top to bottom in the stated environment and
  its outputs inspected.
- Every number in each report was copied from the executed notebook and
  cross-checked against the saved `results/` tables.
- Methodological choices (stratification, fitting transformers on the training
  split only, choosing thresholds on out-of-fold training predictions rather
  than the test set, de-duplication before splitting, splitting captions by
  image) were checked against the assignment brief and course material.
- Claims in the analysis sections were checked against the produced figures and
  metric tables.

## Responsibility

All experiments, results and analysis in the reports were produced and checked
by the student, who takes full responsibility for the work and can explain it
in a viva. No results, metrics, figures or references were invented. Datasets
were used under their stated licences and are not redistributed in this
repository.
