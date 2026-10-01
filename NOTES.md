# Predicta Notes

## Session 1
- Cloned repo, moved it to Desktop, created folder structure
- Next: create virtual environment, install Python packages

## Session 2: Heart Disease EDA

**Objective**
Understand the UCI Heart Disease (Cleveland) dataset before modelling, so that preprocessing decisions are driven by evidence.

**Data**
- 303 patients, 13 clinical features, one target (`num`, severity 0 to 4).
- Target binarised to disease / no disease (`num` > 0), giving a 54% / 46% split. The classes are close to balanced, so accuracy is a reasonable metric, reported alongside recall and ROC-AUC.

**Data quality**
- 6 missing values (`ca`: 4, `thal`: 2), 0 duplicate rows, no impossible values.
- One extreme cholesterol value (564 mg/dl) that appears genuine, so it was kept.

**Key findings**
- Strongest separators between groups: `thalach` (lower in disease), `oldpeak` (higher in disease), `cp` = 4, `thal` = 7, `exang` = 1, `slope` = 2.
- `trestbps`, `chol` and `fbs` show little separation on their own.

**Preprocessing decisions**
- Impute missing values inside a pipeline, fitted on training data only to avoid leakage.
- One-hot encode categorical features stored as numbers (`cp`, `restecg`, `slope`, `thal`).
- Scale numeric features, which sit on very different ranges.
- Drop the original `num` column before training, since it contains the answer.

**Limitations**
- Small sample (303 patients), so performance estimates will be noisy.
- About 68% of patients are male, so results may not generalise equally to women.
- Single clinical source (Cleveland) and decades-old data.
- Educational project only, not a diagnostic tool.

**Next**
Stratified train/test split, preprocessing pipeline, logistic regression baseline.