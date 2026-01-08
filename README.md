Predicting Homicide Outcomes in Shooting Incidents

Authors: Uri Iron and Adir Bella 

Project Overview
This project focuses on the analysis and prediction of the lethality level of shooting incidents in New York City. The research addresses the binary classification problem of whether a shooting incident ended in the death of the victim (target variable: is_murder). By identifying patterns that lead to fatal outcomes, this work aims to assist law enforcement and social welfare agencies in planning targeted prevention strategies and intelligent resource allocation.



Dataset Description
The research utilizes the NYPD Shooting Incident dataset obtained from data.gov (NYC Open Data).


Records: 29,744 rows.


Features: 21 columns including temporal data (date, hour), spatial data (borough, precinct, coordinates), and demographic details (age, sex, and origin of victims and suspects).



Imbalance: The dataset is characterized by a significant imbalance, as non-fatal incidents outnumber fatal ones.

Repository Structure
The project is organized into the following directory structure:

data/: Contains the datasets used during the project.


raw_data.csv: The original dataset.


X_train.csv, X_test.csv, y_train.csv, y_test.csv: Stratified splits for training and evaluation.


X_test_noisy.csv: Test set with 15% synthetic noise for robustness testing.



notebooks/: Detailed Jupyter notebooks covering the end-to-end pipeline.


01_Data_Ingestion_EDA_and_Splitting: Initial data loading, exploratory analysis, and coordinate restoration.


02_Preprocessing_Modeling_and_Analysis: Feature engineering, hyper-parameter tuning, and model evaluation.


requirements.txt: List of essential Python libraries required for the environment.


README.md: Project documentation.

Methodology
Supervised Learning
The project implemented a double-pipeline architecture to accommodate different algorithmic requirements:


Linear and Distance-Based Pipeline: Involved One-Hot encoding, standard scaling, and explicit removal of features with high Variance Inflation Factor (VIF) to ensure mathematical convergence.


Tree-Based Pipeline: Utilized Label Encoding and preserved "missingness" as a unique value, allowing models to learn from the lack of data as a relevant signal.


Five algorithms were evaluated: CatBoost, Logistic Regression, Decision Tree, Random Forest, and AdaBoost.


Unsupervised Learning

K-Means: Implemented a "Risk Gap" strategy to identify statistical separation between high and low-risk profiles.


DBSCAN: Optimized using the K-Distance Elbow method and Grid Search to identify "Lethal Core" micro-clusters.

Key Results and Insights

Top Model: CatBoost emerged as the optimal model, achieving the highest F1-Score (0.3751) and ROC-AUC (0.6633).


Primary Predictors: Geographical coordinates (X/Y) were the strongest predictors of lethality, followed by "suspect_info_available" and the hour of the incident.



Lethal Hotspots: DBSCAN isolated a specific micro-location ("Cluster 6") with an unprecedented lethality rate of 61.8%, highlighting that crime volume does not always correlate with severity.



Robustness: The model demonstrated high durability, with performance dropping by less than 9% when tested against 15% synthetic noise.


Central Dependencies
The project was developed in Python using the following core libraries:

catboost (Primary classification model)

scikit-learn (Modeling, preprocessing, and evaluation)

pandas and numpy (Data manipulation)

matplotlib and seaborn (Visualization)

imbalanced-learn (Handling class imbalance)

holidays (Feature engineering)
