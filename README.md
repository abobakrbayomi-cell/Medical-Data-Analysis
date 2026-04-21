# Medical Data Analysis: Biochemical & Clinical Characteristics

## 📌 Project Overview

This repository contains the Python source code and statistical analysis pipeline for a retrospective case-control study investigating the biochemical and clinical characteristics of **95 subjects**, stratified into healthy controls, newly diagnosed patients, and treated patients.

The primary objective was to evaluate **therapeutic efficacy** and the **diagnostic performance** of specific biomarkers using rigorous statistical testing and diagnostic-evaluation metrics. The analysis produces publication-quality tables, per-variable comparison figures, ROC curves, correlation plots, and correlation heatmaps — all reproducibly from a single notebook.

> ⚠️ **Data confidentiality:** The original dataset contains private medical records and is **not** included in this repository. The notebook is structured to run on any dataset with a matching schema (see [Expected Data Schema](#-expected-data-schema)).

---

## 🛠️ Technologies & Libraries

The analysis was executed using Python, leveraging the following data-science ecosystem:

- **Data manipulation:** `pandas`, `numpy`
- **Statistical analysis:** `scipy.stats`, `scikit-posthocs`
- **Diagnostic evaluation:** `scikit-learn` (for ROC / AUC / confusion matrix)
- **Visualization:** `matplotlib`, `seaborn`

---

## 🔬 Methodology

### 1. Study Design & Population

The cohort (n = 95) was divided into three distinct groups:

| Group | Label | Size |
|-------|-------|------|
| Healthy Controls | Control | n = 35 |
| Newly Diagnosed Patients | NDP | n = 25 |
| Treated Patients | TP | n = 35 |

Additionally, a **longitudinal paired analysis** was performed on a subset of **20 patients** to monitor biochemical changes pre- and post-treatment.

### 2. Biomarkers Analyzed

The dataset included a panel of 11 variables:

- **Oxidative / inflammation / tumor markers:** Heme Oxygenase-1 (HO-1), Ceruloplasmin (CP), Carcinoembryonic Antigen (CEA)
- **Clinical:** Hemoglobin (Hb), Creatinine, ALT, Age
- **Trace elements:** Copper (Cu), Iron (Fe), Zinc (Zn), Calcium (Ca)

### 3. Statistical Pipeline

The analysis followed a strict statistical workflow:

**Data screening**
- Normality was assessed using the **Shapiro-Wilk test**
- Descriptive statistics: Mean ± SE/SD with distribution summaries (Min, Q1, Median, Q3, Max, Range, IQR) for normal distributions; Median ± SIQR for non-normal distributions

**Hypothesis testing**
- **Parametric:** One-Way ANOVA with **Tukey's HSD** post-hoc
- **Non-parametric:** Kruskal-Wallis H test with **Dunn's test** (Bonferroni-corrected) for pairwise comparisons
- **Longitudinal:** Wilcoxon Signed-Rank Test (paired comparison for pre/post-treatment)
- Post-hoc results are annotated on figures using **Compact Letter Display** (groups sharing a letter are not significantly different)

**Diagnostic evaluation**
- **ROC analysis** across three pairwise group comparisons per biomarker (Control vs NDP, Control vs TP, TP vs NDP)
- **Youden J** statistic used to identify the optimal cut-off; sensitivity, specificity, accuracy, and AUC reported

**Correlations**
- **Pearson's coefficient** for linear relationships
- **Spearman's rank correlation** for monotonic relationships (primary method given non-normality and outliers)
- Per-pair correlation figures (overall + stratified by group) alongside full-matrix heatmaps

---

## 📊 Outputs Generated

Running the notebook produces the following artifacts:

### Tables (Excel)
| File | Content |
|------|---------|
| `Descriptive_Statistics.xlsx` | Tables 1 & 2 — total sample and per-group descriptives |
| `Shapiro_Wilk_Normality.xlsx` | Per-variable, per-group normality assessment |
| `Kruskal_Analysis.xlsx` | Table 3 — Kruskal-Wallis H + Dunn's post-hoc letters |
| `ANOVA_Results.xlsx` | Table 4 — ANOVA F-test + Tukey's post-hoc letters |
| `Wilcoxon_Test_Report.xlsx` | Paired Before/After treatment efficacy |
| `ROC_Analysis_Results.xlsx` | AUC, cut-offs, sensitivity, specificity for all 33 comparisons |
| `correlation_analysis.xlsx` | Pearson + Spearman correlation matrices with p-values |

### Figures (PNG, 300 dpi)
- `sex_distribution.png` — sex composition per group and total
- `heatmap_pearson.png`, `heatmap_spearman.png` — full correlation matrices
- `figures/bar_charts/` — Mean ± SD per variable with post-hoc letters
- `figures/box_plots/` — Median ± SIQR with swarm overlay and mean marker
- `figures/roc_curves/` — three-comparison ROC per biomarker with optimal cut-offs
- `figures/correlations/` — Spearman scatter grids (total sample + per-group)

---

## 📂 Expected Data Schema

The notebook expects two input files at the repository root:

**1. `Data.xlsx`** — main dataset (n=95)
- Sheet name: `Clean Data`
- Required columns: `Group` (values `Group 1`, `Group 2`, `Group 3`), `Sex` (`M`/`F` or `Male`/`Female`), and the 11 biomarker columns listed above

**2. `matched group1&2.xlsx`** — paired longitudinal subset (n=20)
- Stacked layout: a row containing `Group 2 - Newly Diagnosed`, followed by headers and 20 rows of before-treatment data, then a row containing `Group 3 - Treated`, followed by headers and 20 rows of after-treatment data
- Subjects are matched across sections by the `Name` column

Column names and the group-code mapping can be customized by editing the constants at the top of the **"Load and Clean Data"** cell (`NUMERIC_COLS`, `GROUP_MAP`, `GROUP_ORDER`).

---

## ▶️ Running the Notebook

```bash
# 1. Clone the repository
git clone <repo-url>
cd <repo-name>

# 2. Install dependencies
pip install pandas numpy scipy scikit-learn scikit-posthocs matplotlib seaborn openpyxl

# 3. Place your data files at the repository root
#    - Data.xlsx (sheet: "Clean Data")
#    - matched group1&2.xlsx

# 4. Launch the notebook
jupyter notebook Medical_Data_Analysis_Project.ipynb
```

Execute cells sequentially from top to bottom. Each analysis section is self-contained and writes its outputs to disk as described above.

---

## 🗂️ Notebook Structure

1. Setup (imports & styling)
2. Load and Clean Data
3. Shared Helpers (p-value formatting, Shapiro-Wilk wrapper, compact-letter-display)
4. Descriptive Statistics — *Tables 1, 2*
5. Sex Distribution
6. Shapiro-Wilk Normality Test
7. Kruskal-Wallis H Test with Dunn's Post-Hoc — *Table 3*
8. One-Way ANOVA with Tukey's Post-Hoc — *Table 4*
9. Wilcoxon Signed-Rank Test — Treatment Efficacy
10. Bar Charts with Post-Hoc Letters
11. Box Plots with Swarm Overlay and Mean Marker
12. ROC Curve Analysis — Plots
13. ROC Results Table
14. Spearman Correlation — Scatter Plots (Overall + per Group)
15. Correlation Heatmaps — Pearson & Spearman

---

## 👤 Author

**Abobakr** — Computer Science (AI specialization) student.

This project was completed as a freelance data-analysis assignment for an academic client. The code has been published for portfolio purposes with the dataset withheld to preserve confidentiality.
