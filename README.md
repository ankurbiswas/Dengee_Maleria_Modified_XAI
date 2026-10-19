# Dengee_Maleria_Modified_XAI

Original analysis notebooks of a PhD project on telling dengue from malaria in Greater Kolkata. The notebooks use routine case line-lists of the Kolkata Municipal Corporation (2014–2022) with six fields (ward, borough, month, age, sex, place of treatment), seven classifiers, three oversampling methods and two explainability tools (SHAP and LIME).

## Contents

| Folder | What it holds |
| --- | --- |
| `Before_Resampling/` | One notebook per classifier (Decision Tree, Random Forest, XGBoost, k-NN, Logistic Regression, MLP, Gaussian Naive Bayes) on the original, imbalanced data, and `DT_leakage_safe_full_test_eval.ipynb`, a Decision Tree evaluation on the full test set with the ward encoded inside the training folds. |
| `SMOTE/`, `BSMOTE/`, `ADASYN/` | For each oversampling method: `Imbalance_*.ipynb`, which writes a `*_balanced_dataset.csv`; one notebook per classifier that reads that file; and `DT_gold_standard_raw_pipeline.ipynb`, the leakage-safe Decision Tree pipeline. |

## Data

The data are patient-level and are not in this repository. `.gitignore` blocks CSV, Excel and archive files so that they cannot be committed by accident. The notebooks expect the files they read (for example `adasyn_balanced_dataset.csv`) in the working folder.

Cell outputs were cleared before the notebooks were added. They were about 20 MB per notebook and could contain patient-level rows. Run a notebook to regenerate its output.

## Packages

numpy, pandas, scipy, scikit-learn, imbalanced-learn, xgboost, shap, lime, matplotlib and seaborn.

## Known issues

- **Data leakage in the original workflow.** In the classifier notebooks, except the two leakage-safe Decision Tree notebooks named above, the ward risk is encoded with the labels of all cases, training and test together. The `Imbalance_*` notebooks also oversample the whole dataset before it is split, so the test set is balanced and about half synthetic. Accuracies from these notebooks cannot be read as estimates of performance on real cases. A leakage-safe re-implementation is kept outside this repository.
- **File names.** `ADASYN/GaussianNB_modified_Using_BSMOTE.ipynb` and `ADASYN/RF_modified_Using_BSMOTE.ipynb` have BSMOTE in their names but read `adasyn_balanced_dataset.csv`.
