# Introduction to Data Science - Article Analysis & Replication (FER)

This repository contains coursework for **Introduction to Data Science (UZOP)** at FER.  
The main focus is a deep-dive replication and critique of the paper:

- **Paper (Durham Repository):** https://durham-repository.worktribe.com/output/1140702/early-predictor-for-student-success-based-on-behavioural-and-demographical-indicators  
- Local copy: `article/EarlyPredictorforStudentSuccessBasedon.pdf`

We reproduce the core modeling setup, evaluate it under a transparent and reproducible pipeline, and document multiple **reproducibility and reporting issues** found in the original work.

---

## Dataset (OULAD)
The paper uses the **Open University Learning Analytics Dataset (OULAD)**.

- **Kaggle (OULAD):** https://www.kaggle.com/datasets/anlgrbz/student-demographics-online-education-dataoulad  
- **Official OULAD page (OU Analyse):** https://analyse.kmi.open.ac.uk/open-dataset

---

## What this repo is about (high-level)
Across three lab projects, we:
- practice core data-wrangling/EDA workflows on a small dataset (Project 1),
- prepare and analyze the OULAD-derived dataset used for early student success prediction (Project 2),
- **replicate and stress-test the paper’s results**, then extend the work with stronger baselines, tuning, feature engineering and additional analyses (Project 3).

The most important deliverable is **Project 3**, which contains the replication + critique + improvements.

---

## Key contributions & takeaways (Project 3)

### 1) Replication (as close as possible to the paper)
- Follow the **One-vs-Rest** setup for the 4-class target (*Withdrawn / Fail / Pass / Distinction*).
- Train baseline tree models (Decision Tree, Random Forest) and a modern tree-ensemble **as a practical substitute for BART** (due to Python/library constraints).
- Evaluate using the same family of metrics mentioned in the paper (precision, recall, F1, accuracy) and inspect confusion matrices + ROC/AUC behavior.

### 2) Reproducibility and reporting issues found in the paper
While ROC curves are broadly consistent (suggesting similar ranking/separation behavior), we identify substantial issues that prevent a faithful, exact replication:
- **Unexplained data filtering / inconsistent dataset size**: the paper’s reported test-set size does not match what a standard 70/30 split yields on the stated dataset size, implying additional filtering steps that are not documented.
- **Metric inconsistencies**: values reported for precision/recall do not align with the confusion matrix shown in the paper, indicating clear reporting/calculation errors.
- **Insufficient preprocessing documentation**: missing-value handling and filtering rules are not described in enough detail to reproduce the exact table-level results.

### 3) Improvements / extensions
We then go beyond replication to test what actually improves performance and robustness:
- **Hyperparameter tuning** (systematic search rather than defaults)
- **Feature engineering** using signals available *before* or *around* the first assessment (e.g., activity-day features, click aggregates, “submitted first assignment”, etc.)
- **Alternative models** (linear + non-linear baselines and stronger ensembles)
- **Class imbalance handling** (SMOTE) and its effect on minority-class recall/F1
- **Temporal signal analysis**: prediction quality improves when using data from later points in the course (expected), supporting stage-based interventions.
- **Course/module heterogeneity**: training per-module models yields noticeably better F1, suggesting that “one global model” hides important differences between courses.

---

## Repository structure
```text
Introduction-to-data-science/
├─ article/
│  └─ EarlyPredictorforStudentSuccessBasedon.pdf
├─ UZOP_Projekt_1/
│  ├─ climate_change_impact_on_agriculture_2025.csv
│  └─ Galic_Fran_0036546889_1.ipynb
├─ UZOP_Projekt_2/
│  ├─ anonymisedData/
│  ├─ processed_data/
│  │  ├─ early_predictors_final.csv
│  │  ├─ early_predictors_final.parquet
│  │  ├─ early_predictors_ml.csv
│  │  ├─ early_predictors_ml.parquet
│  │  └─ early_predictors_ml_transformations.txt
│  └─ Galic_Fran_0036546889_projekt2.ipynb
├─ UZOP_Projekt_3/
│  ├─ processed_data/
│  │  └─ early_predictors_all_features.csv
│  └─ Galic_Fran_0036546889_projekt3.ipynb
├─ .python-version
├─ LICENSE
├─ pyproject.toml
├─ uv.lock
└─ README.md
```
---

## How to run
This repository uses a reproducible Python environment defined by `pyproject.toml` and `uv.lock`.

### 1) Set up environment (recommended)
```bash
uv sync
```

### 2) Launch notebooks
```bash
uv run jupyter lab
```

Then open the corresponding notebook:
- `UZOP_Projekt_1/Galic_Fran_0036546889_1.ipynb`
- `UZOP_Projekt_2/Galic_Fran_0036546889_projekt2.ipynb`
- `UZOP_Projekt_3/Galic_Fran_0036546889_projekt3.ipynb`  ← main deliverable

> Note: If any notebook expects local paths for anonymised/raw data, adjust them to your machine.

---

## Project overview

### Project 1 - Warm-up (data wrangling + EDA)
A small-scale practice notebook focused on:
- cleaning and transforming a dataset,
- basic descriptive statistics,
- quick visual exploration.

### Project 2 - Data preparation for the paper task (OULAD-derived)
Focus on:
- building a clean “model-ready” table,
- handling missingness and categorical encodings,
- documenting transformations (`processed_data/*` + transformation notes).

### Project 3 - Replication, critique, and improvements (main)
Focus on:
- reproducing the modeling setup from the paper,
- verifying reported metrics and confusion matrices,
- diagnosing reproducibility gaps,
- running improvements: tuning, feature engineering, alternative models, imbalance handling,
- additional analyses: time-based prediction strength and per-course heterogeneity.

---

## Academic / ethical note
This repository is intended for educational purposes (coursework).  
If you reuse the paper, dataset, or any of the analysis ideas, please cite the original sources and follow FER rules on academic integrity.

---

## License
See `LICENSE`.