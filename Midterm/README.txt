# Midterm Project — Stroke Risk Prediction: Data Cleanup & Preprocessing

**Course:** ITAI 1371 — Machine Learning
**Team:** Karima, Danh, Great, Quan, Camila
**Target variable:** `Stroke` (0 = no stroke, 1 = stroke)

## Overview
This project takes a patient health dataset through a complete, reproducible preprocessing pipeline in Python and shows the data **before and after** each step. The cleaned data will be used in the final project to train and compare machine-learning models that predict stroke.

All changes to the data are made in code. **The dataset was never edited manually or in Excel.**

## Dataset
- **Original source (Kaggle):** https://www.kaggle.com/datasets/rafi003/healthcare-disease-prediction-dataset?resource=download>
- **Working copy (Google Sheets):** https://docs.google.com/spreadsheets/d/1wQTS2-bZKC2n17To2Smp1NAFMFeBEjh_rklu0wi7mu0/edit?gid=1445603174
- **Size:** 2,000 rows × 15 columns (14 after dropping the `Patient_ID` identifier)
- **Features:** Age, Gender, BMI, Blood_Pressure_Systolic, Blood_Pressure_Diastolic, Cholesterol, Glucose_Level, Smoking, Alcohol_Intake, Physical_Activity, Family_History, Heart_Disease, Diabetes
- **Target:** Stroke (about 5% positive, so the classes are heavily imbalanced)

The URL of the original dataset is also saved by the notebook in `dataset_url.txt`.

## Repository contents
| File | Description |
|---|---|
| `Stroke_Preprocessing_Midterm.ipynb` | Main notebook: split, EDA, cleanup, before/after plots, baseline models |
| `dataset_url.txt` | URL of the original dataset |
| `train_processed.csv` | Cleaned, encoded, engineered and scaled training set (70%) |
| `test_processed.csv` | Test set (30%) with the same transformations applied |
| `train_balanced_smotenc.csv` | Training set after class balancing with SMOTE-NC |
| `Dataset_Proposal.pdf` | One-page dataset description and project proposal |
| Reflection journal / Contribution journal | Team documents (see course submission list) |

## Pipeline (in notebook order)
1. **Load** the data from Google Sheets (or a local CSV); confirm at least 2,000 rows.
2. **Split** 70% train / 30% test, stratified, in Python. The test set is held out.
3. **Inspect and explore** the training set only: types, missing values, distributions, correlations, matplotlib plots.
4. **Missing and invalid values:** implausible BMI values (below 15) are set to NaN and filled with the training median.
5. **Encoding:** `Gender` one-hot encoded.
6. **Feature engineering:** Pulse_Pressure, MAP, BMI_Category, BP_Risk_Category, BP_Inverted_Flag, Age_60_Plus, High_Cholesterol, High_Glucose.
7. **Normalization and scaling:** Yeo-Johnson transform for skewed columns (only if needed), then StandardScaler.
8. **Class balancing:** SMOTE-NC on the training set only.
9. **Baseline models:** Logistic Regression and Random Forest, with and without balancing.
10. **Export** the processed files.

Every learned step (imputer, transformer, scaler, SMOTE-NC) is fit on the training data only and then applied to the test data, so no information leaks from test to train.

## How to run
**Google Colab (recommended)**
1. Upload `Stroke_Preprocessing_Midterm.ipynb` to https://colab.research.google.com.
2. Make sure the Google Sheet is shared as "Anyone with the link can view".
3. Run **Runtime → Run all**.
4. Output files appear in the Colab Files panel (`content` folder). Download them before the session ends.

**Local Jupyter**
```bash
pip install pandas numpy matplotlib scikit-learn imbalanced-learn jupyter
jupyter notebook Stroke_Preprocessing_Midterm.ipynb
```
To work offline, save the dataset as `stroke_dataset.csv` next to the notebook.

## Requirements
Python 3.9+, pandas, numpy, matplotlib, scikit-learn, imbalanced-learn.

## Notes and limitations
- Stroke is rare, so accuracy is not used as the main metric. We report precision, recall, F1 and ROC-AUC for the stroke class.
- The notebook includes a check of whether a single threshold rule reproduces the target. If it does, the data is likely synthetic, and high model scores reflect how the data was built rather than real-world performance.
- SMOTE-NC creates synthetic patients and is never applied to the test set.
