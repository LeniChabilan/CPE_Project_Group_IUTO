# CPE_Project_Group_IUTO

## Project Title
Predicting Heart Disease from Clinical Measurements

## Summary
This project uses the UCI Cleveland Heart Disease dataset (via Kaggle) to predict whether a patient has heart disease based on 13 standard clinical measurements (age, blood pressure, cholesterol, maximum heart rate, chest pain type, etc.). After discovering and removing 723 duplicate rows and 6 rows with invalid category codes from the raw 1,025-row file, we trained and compared four classification models — Logistic Regression, K-Nearest Neighbors, Decision Tree, and Random Forest — on the resulting 296 unique patient records. Logistic Regression gave the best overall trade-off (F1-score ≈ 0.82, accuracy ≈ 0.80, AUC ≈ 0.87), with chest pain type, ST depression, number of major vessels, thalassemia result, and maximum heart rate identified as the most informative predictors.

## Group Information
- **Group:** IUTO
- **Course:** CPE393 — Introduction to Data Science with Python, Summer 2026, KMUTT

**Members:**
| Name | Student ID |
|------|-----------|
| Leni Chabilan | 25560730035 |
| Kylian Riberou | 25560730059 |
| Romain Mechain | 25560730052 |

## Dataset
- **Source:** Kaggle — Heart Disease Dataset (based on the UCI Heart Disease / Cleveland database): https://www.kaggle.com/datasets/johnsmith88/heart-disease-dataset 
- **Description:** Clinical data for patients evaluated for heart disease, containing 13 explanatory variables (demographics, resting clinical measurements, and exercise-related measurements) plus a binary target indicating the presence of heart disease.
- **License / usage condition:** Publicly available on Kaggle for academic/educational use (originally derived from the UCI Machine Learning Repository, Cleveland database).
- **Rows / Columns:** Raw file: 1,025 rows × 14 columns. After removing 723 exact duplicates and 6 rows with invalid category codes: 296 unique patient records × 14 columns (19 after one-hot encoding).
- **Target variable:** `target` (0 = no heart disease, 1 = heart disease present)


## Repository Structure
```
CPE_Project_GroupIUTO/
├── README.md
├── project_notebook.ipynb
├── project_summary.pdf
├── presentation_slides.pdf
├── requirements.txt
├── data/
│   └── data_link.txt
├── figures/
└── (other supporting files)
```

## How to Run the Notebook
1. Clone this repository:
   ```bash
   git clone <repo-url>
   cd CPE_Project_Group_IUTO
   ```
2. (Recommended) Create and activate a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # on Windows: venv\Scripts\activate
   ```
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Open and run `project_notebook.ipynb` in Jupyter Notebook, JupyterLab, VS Code, or upload it to Google Colab.

## Required Libraries / Environment
- Python 3.9+
- NumPy, Pandas — data loading, cleaning, and transformation
- Matplotlib, Seaborn — data visualization
- scikit-learn — preprocessing (StandardScaler, one-hot encoding), model training (Logistic Regression, KNN, Decision Tree, Random Forest), cross-validation, and evaluation metrics (accuracy, precision, recall, F1-score, confusion matrix, ROC/AUC)
- See `requirements.txt` for the full pinned list

## Main Results
- After cleaning (removing 723 duplicate rows and 6 rows with invalid category codes), 296 unique patients remained, with a reasonably balanced target (≈54% disease / 46% healthy).
- Four classification models were trained and compared using 5-fold stratified cross-validation and a held-out test set (60 patients, 20%):

| Model | Accuracy | Precision | Recall | F1-score | AUC |
|---|---|---|---|---|---|
| Logistic Regression | 0.800 | 0.778 | 0.875 | 0.824 | 0.868 |
| KNN (k=7) | 0.767 | 0.750 | 0.844 | 0.794 | 0.837 |
| Random Forest | 0.750 | 0.743 | 0.812 | 0.776 | 0.846 |
| Decision Tree | 0.717 | 0.727 | 0.750 | 0.738 | 0.794 |

- **Logistic Regression** achieved the best overall trade-off, correctly identifying about 88% of patients who actually had heart disease (recall = 0.875).
- The most informative predictors were chest pain type (`cp`), ST depression (`oldpeak`), number of major vessels (`ca`), thalassemia result (`thal`), and maximum heart rate (`thalach`) — consistent with clinical knowledge.

## Limitations
- The raw Kaggle file contained 70% duplicate rows; training on the uncleaned data (as many public notebooks do) produces artificially inflated accuracy (~92%) due to data leakage. Our results, computed after proper cleaning, are more modest but more trustworthy.
- After cleaning, only 296 patients remain, all from a single clinical study (Cleveland), which limits statistical power and generalization to other populations or healthcare systems.
- The dataset does not document the precise geographic or demographic origin of the patients.
- The dataset contains far more male (201) than female (95) patients, producing a counter-intuitive sex/disease relationship in this sample (74.7% of women vs. 44.3% of men diagnosed) that is likely a sampling artifact rather than a real medical trend.
- The held-out test set is small (60 patients), so differences between models should be interpreted cautiously rather than as a definitive ranking.
- This project is educational and exploratory; the models should never be used as a substitute for professional medical diagnosis.
