# ME/CFS Classification and Analysis Project

## Overview

This project develops machine learning models to **predict and classify Myalgic Encephalomyelitis/Chronic Fatigue Syndrome (ME/CFS)** status using clinical survey data and multi-omics datasets. The goal is to identify predictive biomarkers and symptom patterns that differentiate ME/CFS patients from healthy controls.

## Project Background

Myalgic Encephalomyelitis/Chronic Fatigue Syndrome (ME/CFS) is a complex chronic illness characterized by:
- Severe fatigue not relieved by rest
- Post-exertional malaise (PEM)
- Cognitive dysfunction ("brain fog")
- Unrefreshing sleep
- Various other symptoms (pain, sore throat, etc.)

This project uses machine learning to identify key symptoms and biomarkers that can help classify individuals as ME/CFS patients or controls.

## Repository Structure

```
ProjectME/
├── code/                          # Main analysis code
│   ├── cmps262project (1).py      # Primary data preprocessing and feature engineering
│   ├── cmps262project (4).ipynb   # Comprehensive analysis notebook
│   ├── code2.ipynb                # Secondary analysis
│   ├── Dataset1.ipynb             # Dataset exploration
│   ├── X_train.csv                # Training features
│   ├── X_test.csv                 # Testing features
│   ├── y_train.csv                # Training labels
│   ├── y_test.csv                 # Testing labels
│   ├── Clean_survey_phenotype.csv # Cleaned survey data
│   └── FeatureEngineered_survey_phenotype_dataset.csv  # Data with engineered features
│
├── datasets/                      # Raw datasets
│   ├── 1.medical_data.csv         # General medical data
│   ├── 2.me_cfs_vs_depression_dataset.csv  # ME/CFS vs Depression comparison
│   ├── 3.12-Month_follow_up_Dataset/      # Longitudinal follow-up data
│   ├── 4.study_data_mecfs_metabolomics.xlsx # Metabolomics data
│   └── 6. RNA seq datasets/       # RNA-sequencing data
│
├── presentations/                 # Project presentations
│   ├── Milestone1 presentation.pdf
│   └── Final presentation.pdf
│
├── Final project report.pdf       # Comprehensive final report
└── README.md                      # This file
```

## Key Features

### Data Processing Pipeline

1. **Data Cleaning**
   - One-hot encoding for categorical variables
   - Missing value imputation using K-Nearest Neighbors (KNN)
   - Removal of redundant and pharmacokinetic features
   - Handling of structural missing values

2. **Sample Handling**
   - Participants had multiple survey entries over time
   - Used **GroupShuffleSplit** to prevent data leakage
   - Ensures no participant appears in both training and testing sets

### Feature Engineering

The project creates composite features from raw symptoms:

- **Total Symptom Score**: Sum of key symptoms (Fatigue, Brain Fog, PEM, Sleep Disturbance)
- **Physical Cluster**: Average of physical symptoms (Myalgia, Arthralgia, Tender Nodes)
- **Neurological Cluster**: Average of neurological symptoms (Fatigue, Brain Fog, Sleep Disturbance)
- **PEM-Recovery Interaction**: Product term capturing relationship between PEM and recovery time

### Core Symptoms Analyzed

- Fatigue
- Brain Fog (Cognitive Dysfunction)
- Post-Exertional Malaise (PEM)
- Sleep Disturbance
- Myalgia (Muscle Pain)
- Arthralgia (Joint Pain)
- Headache
- Sore Throat
- Tender Nodes

## Machine Learning Models

The project evaluates six different classification algorithms:

| Model | Type | Use Case |
|-------|------|----------|
| **Gradient Boosting Classifier (GBC)** | Ensemble | Best overall performance |
| **Random Forest (RF)** | Ensemble | Feature importance analysis |
| **XGBoost (XGB)** | Gradient Boosting | High-performance classification |
| **Support Vector Machine (SVM)** | Kernel-based | Non-linear decision boundaries |
| **K-Nearest Neighbors (KNN)** | Instance-based | Simple baseline comparison |
| **Logistic Regression (LR)** | Linear | Interpretable baseline |

### Model Selection

Hyperparameter tuning performed using **GridSearchCV** with 5-fold cross-validation. Feature selection conducted using **Lasso regression** to handle multicollinearity.

## Key Findings

### Model Performance
- Near-perfect classification accuracy achieved on test set
- High F-beta scores emphasizing sensitivity (recall)
- Careful attention to false negatives (misclassifying ME/CFS as control)

### Feature Importance
- Top performing features identified through permutation importance
- Analysis of both original and engineered features
- Sensitivity and specificity metrics calculated

### Clinical Insights
- Certain symptom combinations strongly predictive of ME/CFS status
- Participants showed varying engagement levels (some repeated surveys 14+ times)
- Physical symptom clusters show distinct patterns in ME/CFS vs controls

## Datasets Used

1. **Survey Phenotype Data**: Primary dataset with symptom ratings and participant metadata
2. **Medical Data**: General clinical information
3. **ME/CFS vs Depression Data**: Comparative analysis with depression patients
4. **12-Month Follow-up Data**: Longitudinal tracking of disease progression
5. **Metabolomics Data**: Biochemical markers
6. **RNA-Sequencing Data**: Gene expression profiles (30+ samples)

## Requirements

```
pandas
numpy
scikit-learn
xgboost
matplotlib
seaborn
```

## Usage

### Data Preparation
```bash
python cmps262project\ \(1\).py
```
This script:
- Loads and cleans the survey phenotype data
- Performs feature engineering
- Creates train/test splits
- Saves processed datasets

### Model Training and Evaluation
Run the Jupyter notebook:
```bash
jupyter notebook code/cmps262project\ \(4\).ipynb
```

This notebook includes:
- Exploratory data analysis
- Model training and hyperparameter tuning
- Performance evaluation
- Feature importance analysis

## Methodology Highlights

### Cross-Validation Strategy
- **GroupShuffleSplit**: Prevents participant leakage between train/test sets
- **5-fold CV**: Standard cross-validation for hyperparameter tuning
- **F-Beta Scoring**: Emphasizes minimizing false negatives in medical context

### Evaluation Metrics
- Accuracy
- Precision & Recall
- F1-Score & F-Beta Score
- ROC-AUC
- Confusion Matrix
- Sensitivity & Specificity

## Results Interpretation

The model's primary objective is **maximizing sensitivity** (true positive rate) to avoid missing ME/CFS diagnoses. While maintaining reasonable specificity, the focus is on reducing false negatives—cases where ME/CFS patients are incorrectly classified as healthy controls.

## Files Description

| File | Purpose |
|------|---------|
| `Clean_survey_phenotype.csv` | Cleaned dataset with imputed values |
| `FeatureEngineered_survey_phenotype_dataset.csv` | Dataset with calculated features |
| `selected_features.csv` | Features selected by Lasso regression |
| `X_train.csv`, `X_test.csv` | Feature matrices for training/testing |
| `y_train.csv`, `y_test.csv` | Target labels (ME/CFS vs Control) |

## Future Directions

1. **Validation on External Cohorts**: Test model on independent ME/CFS populations
2. **Temporal Analysis**: Leverage longitudinal data for progression prediction
3. **Multi-Omics Integration**: Combine survey data with metabolomics and RNA-seq
4. **Deployment Framework**: Create clinical decision support tool
5. **Explainability**: Enhanced interpretability for clinician adoption

## References

This project analyzes ME/CFS using the Revised Canadian Consensus Criteria, incorporating standardized symptom assessment and longitudinal follow-up protocols.

---

## Contact & Attribution

**Project Type**: Capstone Project
**Status**: Complete with final report and presentations

For detailed methodology and results, refer to:
- `Final project report.pdf` - Comprehensive technical documentation
- `presentations/Final presentation.pdf` - Summary of key findings

---

*Last Updated: November 2025*
