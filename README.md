# Identifying Sequencing Depth Bias in Lung Cancer scRNA-seq Data (GSE131907)

## Overview
This project analyzes a public lung cancer single-cell RNA-seq (scRNA-seq) cohort (GSE131907) using Python.  
The focus is on **cleaning sample-level metadata**, performing exploratory analysis, and identifying a key methodological issue in scRNA-seq studies: **unequal sequencing depth (cells per sample)**.

## Why this project
Single-cell RNA-seq studies often compare clinical groups (e.g., cancer stage, smoking status). However, if the **number of cells sequenced per sample varies widely**, downstream results (tumor heterogeneity, tumor–immune comparisons) may be biased because samples with more cells can dominate analyses.

This repo demonstrates:
- Real-world biomedical data cleaning (messy GEO table → clean dataset)
- Exploratory cohort profiling
- Evidence of sequencing depth variability across samples and stages
- A clear, reproducible workflow with plots

---

## Dataset
- **Source:** GEO (GSE131907)
- **Cancer Type:** Lung adenocarcinoma
- **Data used in this repo:** Sample-level / clinical metadata including:
  - Patient id, Sample id
  - Sex, Age
  - Smoking status
  - Cancer stage
  - Number of single-cells per sample

> Note: This is **public data**, so IRB approval is not required.

---

## What I did (Workflow)
1. **Loaded the raw cohort table** exported from GEO
2. **Fixed malformed headers** and removed blank rows
3. **Converted numeric columns** (Age, No. of single-cells)
4. **Exploratory Data Analysis (EDA)**
   - Patients and sample counts
   - Stage distribution
   - Smoking status distribution
   - Summary statistics for cell counts
5. **Visualization**
   - Bar chart: stage distribution
   - Bar chart: smoking status distribution
   - Histogram: cells per sample
   - Boxplot: cells per sample by cancer stage (**key evidence plot**)
6. **Saved clean analysis-ready dataset**

---

## Key Results (from this cohort)
- **44 unique patients**
- **58 unique samples**
- Cancer stages range from early (IA) to advanced (IV)
- **Single-cell sequencing depth varies widely across samples**
  - Min ≈ 1,070 cells
  - Max ≈ 5,798 cells
  - Mean ≈ 3,595 cells

---

## Key Insight (Gap Identified)
**Unequal sequencing depth** exists even within the same cancer stage.  
This can bias downstream scRNA-seq analyses if not reported or adjusted for.

### Recommendation
Single-cell studies should:
- Report sequencing depth per sample
- Apply minimum cell-count thresholds and/or normalization strategies
- Consider weighting approaches when comparing clinical groups

---

## Tech Stack
- Python
- pandas
- matplotlib

---

## Repository Structure (suggested)

# projects
├── data/
│ ├── GSE131907_Lung_Cancer_Feature_Summary.csv
│ └── GSE131907_clean_sample_summary.csv
├── notebooks/
│ └── lung_scrnaseq_depth_bias_analysis.ipynb
├── outputs/
│ ├── stage_distribution.png
│ ├── smoking_status.png
│ ├── cells_histogram.png
│ └── cells_by_stage_boxplot.png
└── README.md

---

## How to Run
1. Clone the repo
2. Open the notebook in Google Colab or Jupyter
3. Install dependencies if needed:
```bash
pip install pandas matplotlib
