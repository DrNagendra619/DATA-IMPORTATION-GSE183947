# DATA-IMPORT-GSE183947
DATA IMPORTATION
# 🔬 Gene Expression Data Analysis: GSE183947 FPKM Data

## 📝 Overview

This project notebook performs fundamental Exploratory Data Analysis (EDA) on the **GSE183947** gene expression dataset, specifically the **FPKM** (Fragments Per Kilobase of transcript per Million mapped reads) matrix.

The workflow covers essential steps for handling high-dimensional biological data, including data loading, inspection, cleaning, filtering for expressed genes, performing data transformation (log-normalization), and visualizing gene expression distributions and variability.

## 🚀 Analysis Workflow

The Jupyter Notebook executes the following key steps using the `pandas`, `numpy`, `matplotlib`, and `seaborn` libraries:

### 1. Data Import and Inspection

* **Libraries**: Imports necessary libraries for data manipulation and visualization (`pandas`, `matplotlib.pyplot`, `seaborn`, `numpy`).
* **Data Loading**: Reads the gene expression data from the file `GSE183947_fpkm.csv` into a pandas DataFrame.
* **Initial Check**: Uses `df.head()` and `df.info()` to verify column structure, data types, and check for null values (all non-null).
    * **Data Size**: The original dataset contains **20,246 rows** (genes) and **61 columns** (samples + gene names).
    * **Structure**: Columns appear to follow a naming convention like `CA.XXXXXX` and `CAP.XXXXXX`, likely representing different conditions or sample types.

### 2. Data Cleaning and Filtering

* **Index Setting**: The first column, labeled `'Unnamed: 0'` (which contains **gene names**), is set as the DataFrame index for easier gene-based analysis.
* **Low Expression Filtering**: The DataFrame is filtered to keep only genes with an **average FPKM expression greater than 1** across all samples (`df.mean(axis=1) > 1`). This removes lowly or unexpressed genes, which often simplifies and improves downstream analysis.

### 3. Visualization and Transformation

* **FPKM Distribution (Pre-Log)**: A histogram and KDE plot are generated for all FPKM values across the filtered dataset (`df_filtered`) to visualize the initial data distribution. This typically reveals a highly skewed distribution.
* **Variance Calculation**: A new column, `'var'`, is added to the filtered DataFrame to store the **variance** of FPKM values for each gene.
* **Highly Variable Gene (HVG) Heatmap**:
    * The top **50 most variable genes** (`top_var_genes`) are selected based on the variance score.
    * A **heatmap** is generated using `seaborn` to visualize the expression patterns of these HVGs across all samples. This visualization is critical for identifying gene sets that distinguish between sample groups.
* **Log-Normalization**: FPKM values are transformed using the $\log_2(x+1)$ formula ($\log_2(\text{FPKM} + 1)$). This is a standard practice in RNA-Seq analysis to stabilize variance and normalize the heavily skewed data distribution.

## 💾 Data

* **Primary Data File**: `GSE183947_fpkm.csv`
* **Source**: Assumed to be **FPKM** (Fragments Per Kilobase of transcript per Million mapped reads) data from the GEO accession **GSE183947**.

## 🛠️ Requirements

The notebook requires the following Python libraries:

```bash
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
