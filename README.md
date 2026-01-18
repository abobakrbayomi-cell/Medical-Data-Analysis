# Medical Data Analysis: Biochemical & Clinical Characteristics

## 📌 Project Overview
This repository contains the Python source code and statistical analysis pipeline for a retrospective case-control study. The project investigates the biochemical and clinical characteristics of **95 subjects**, stratified into healthy controls, newly diagnosed patients, and treated patients.

The primary objective was to evaluate therapeutic efficacy and diagnostic performance of specific biomarkers using rigorous statistical testing and machine learning evaluation metrics.

> **⚠️ Important Note:** The original dataset used in this analysis contains private medical records and **is not included** in this repository to protect patient confidentiality. The code is structured to run on datasets with a similar schema.

## 🛠️ Technologies & Libraries
The analysis was executed using Python, leveraging the following data science ecosystem:
* **Data Manipulation:** `pandas`, `numpy`
* **Statistical Analysis:** `scipy.stats`, `scikit-posthocs`
* **Visualization:** `matplotlib`, `seaborn`
* **Machine Learning (Metrics):** `scikit-learn`

## 🔬 Methodology

### 1. Study Design & Population
The cohort (n=95) was divided into three distinct groups:
1.  **Healthy Controls:** (n = 35)
2.  **Newly Diagnosed Patients:** (n = 25)
3.  **Treated Patients:** (n = 35)

Additionally, a **longitudinal analysis** was performed on a specific subset of 20 patients to monitor changes pre- and post-treatment.

### 2. Biomarkers Analyzed
The dataset included a comprehensive panel of markers:
* **Biochemical:** Heme Oxygenase-1 (HO-1), Ceruloplasmin (CP), CEA, Hemoglobin (Hb), Creatinine, ALT.
* **Trace Elements:** Copper (Cu), Iron (Fe), Zinc (Zn), Calcium (Ca).

### 3. Statistical Pipeline
The analysis followed a strict statistical workflow:

* **Data Screening:**
    * Normality was assessed using the **Shapiro-Wilk test**.
    * Homogeneity of variances was checked using **Levene’s test**.
    * Data summary: Mean ± SE/SD for normal distributions; Median (IQR) for non-normal distributions.

* **Hypothesis Testing:**
    * **Parametric:** One-Way ANOVA (for normally distributed data).
    * **Non-Parametric:** Kruskal-Wallis H test (for non-normal data/outliers) followed by **Dunn’s test** for pairwise comparisons.
    * **Longitudinal:** Wilcoxon Signed-Rank Test (paired comparison for pre/post-treatment).

* **Diagnostic Evaluation:**
    * **ROC Analysis:** Calculation of AUC, sensitivity, and specificity to determine optimal cut-off values.

* **Correlations:**
    * **Pearson’s coefficient:** For linear relationships.
    * **Spearman’s rank correlation:** For monotonic relationships (visualized via heatmaps).

## 📊 Visualization
The project includes various visualizations to interpret the data:
* **Distribution Plots:** To inspect data spread and normality.
* **Boxplots:** To visualize group differences and outliers.
* **Correlation Heatmaps:** To display relationships between clinical variables.
