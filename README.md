# Predicting Homicide Outcomes in Shooting Incidents

[cite_start]**Authors:** Uri Iron and Adir Bella [cite: 135, 136, 299]

---

## Project Overview
[cite_start]This project focuses on the analysis and prediction of the lethality level of shooting incidents in New York City[cite: 139]. [cite_start]The research addresses a binary classification problem: determining whether a shooting incident ended in the death of the victim (target variable: `is_murder`)[cite: 140, 302]. [cite_start]By identifying patterns that lead to fatal outcomes, this work aims to assist law enforcement and social welfare agencies in planning targeted prevention strategies and intelligent resource allocation[cite: 143, 306].

## Dataset Description
* [cite_start]**Source:** The research utilizes the NYPD Shooting Incident dataset obtained from **data.gov** (NYC Open Data)[cite: 154, 300].
* [cite_start]**Records:** 29,744 individual shooting records[cite: 155, 303].
* [cite_start]**Features:** 21 columns including temporal data (date, hour), spatial data (borough, precinct, coordinates), and demographic details (age, sex, and origin of victims and suspects)[cite: 156, 301].
* [cite_start]**Imbalance:** The dataset is characterized by a significant class imbalance, as non-fatal incidents far outnumber fatal ones[cite: 141, 190].

## Repository Structure
The project is organized into the following directory structure (as shown in the repository):

* **`data/`**: Contains the datasets used during the project.
    * `raw_data.csv`: The original dataset.
    * `X_train.csv`, `X_test.csv`, `y_train.csv`, `y_test.csv`: Stratified splits for training and evaluation.
    * `X_test_noisy.csv`: Test set with 15% synthetic noise for robustness testing.
* **`notebooks/`**: Detailed Jupyter notebooks covering the end-to-end pipeline.
    * `01_Data_Ingestion_EDA_and_Splitting`: Initial data loading, exploratory analysis, and coordinate restoration.
    * `02_Preprocessing_Modeling_and_Analysis`: Feature engineering, hyper-parameter tuning, and model evaluation.
* [cite_start]**`requirements.txt`**: List of essential Python libraries required for the environment[cite: 50, 92].
* [cite_start]**`README.md`**: Project documentation[cite: 13].

## Methodology

### Supervised Learning
The project implemented a double-pipeline architecture to accommodate different algorithmic requirements:
1.  [cite_start]**Linear and Distance-Based Pipeline:** Involved One-Hot encoding, standard scaling, and explicit removal of features with high Variance Inflation Factor (VIF) to ensure mathematical convergence[cite: 208, 209, 212].
2.  [cite_start]**Tree-Based Pipeline:** Utilized Label Encoding and preserved "missingness" as a unique value, allowing models to learn from the lack of data as a relevant signal[cite: 213, 214, 216].

[cite_start]**Classification Models Evaluated:** CatBoost, Logistic Regression, Decision Tree, Random Forest, and AdaBoost[cite: 218, 219, 220, 221, 222, 223].

### Unsupervised Learning
* [cite_start]**K-Means:** Implemented a "Risk Gap" strategy to identify statistical separation between high and low-risk profiles[cite: 225, 259, 260].
* [cite_start]**DBSCAN:** Optimized using the $K$-Distance Elbow method and Grid Search to identify "Lethal Core" micro-clusters[cite: 226, 263, 264].

## Key Results and Insights
* [cite_start]**Winning Model:** **CatBoost** emerged as the optimal model, achieving the highest **F1-Score (0.3751)** and **ROC-AUC (0.6633)**[cite: 230].
* [cite_start]**Primary Predictors:** Geographical coordinates ($X/Y$) were the strongest predictors of lethality, followed by "suspect_info_available" and the hour of the incident[cite: 253, 275, 276].
* [cite_start]**Lethal Hotspots:** DBSCAN isolated a specific micro-location ("Cluster 6") with an unprecedented lethality rate of **61.8%**, highlighting that crime volume does not always correlate with severity[cite: 266, 267, 278].
* [cite_start]**Robustness:** The model demonstrated high durability, with performance dropping by less than **9%** when tested against 15% synthetic noise[cite: 255, 280].

## Central Dependencies
[cite_start]The project was developed in Python using the following core libraries[cite: 296]:
* `catboost` (Primary classification model)
* `scikit-learn` (Modeling, preprocessing, and evaluation)
* `pandas` & `numpy` (Data manipulation)
* `matplotlib` & `seaborn` (Visualization)
* `imbalanced-learn` (Handling class imbalance)
* `holidays` (Feature engineering)
