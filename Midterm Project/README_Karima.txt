ITAI-1371 Machine Learning Midterm Project
Deliverables prepared for Karima — Data & Split Lead

Source file: Midterm Project Datatset.xlsx
Source sheet: healthcare_disease_prediction_2
Original shared Google Sheet:
https://docs.google.com/spreadsheets/d/1wQTS2-bZKC2n17To2Smp1NAFMFeBEjh_rklu0wi7mu0/edit?gid=1445603174

Original dataset shape: 2000 rows x 15 columns
Training split: 1400 rows (70%)
Testing split: 600 rows (30%)
Split method: train_test_split(test_size=0.30, random_state=42, stratify=df['Stroke'])
Total missing values in original dataset: 0

No missing values were found, so imputation was not necessary. If missing values are
introduced or discovered in later data versions, fit imputers on training data only
and use transform() on test data. Patient_ID is retained in these split files for
traceability; exclude it from model features during modeling. Stroke is the example
classification target used to stratify the split.
