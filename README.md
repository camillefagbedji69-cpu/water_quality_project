# 💧 Water Quality Analysis & Potability Prediction


## 📌 Project Overview

Access to safe drinking water is a fundamental human right. This project evaluates water quality and predicts potability based on chemical and physical properties. Using a refined dataset and optimized Machine Learning workflows, we provide a data-driven approach to distinguish between potable ($1$) and non-potable ($0$) water sources.

## 📊 Dataset & Preprocessing

The study utilizes the `water_potability.csv` dataset (3,276 water bodies) on Kaggle.

* **Data Cleaning**: Rows with missing values were removed to ensure high-fidelity analysis, resulting in **2,011 observations**.
* **Workflow**: Implementation of a **Scikit-Learn Pipeline** with **Cross-Validation** to prevent data leakage and ensure model robustness.

### Key Features (WHO Standards)

* **pH**: Acid-base balance (Target: 6.5 - 8.5).
* **Solids (TDS)**: Total dissolved solids (Desirable < 500 mg/L).
* **Chloramines**: Major disinfectants (Safe up to 4 mg/L).
* **Turbidity**: Water clarity (Max 5.00 NTU).

## 🤖 Model Benchmarking

Six classification architectures were evaluated. Initial results showed that **SVM** and **Random Forest** provided the best baseline performance.

| Model | AUC | Recall | F1-Score |
| --- | --- | --- | --- |
| **SVM** | **0.7248** | 0.3721 | 0.4923 |
| **Random Forest** | 0.6982 | 0.4012 | 0.4964 |
| **XGBoost** | 0.6586 | 0.4477 | 0.5099 |
| AdaBoost | 0.4761 | 0.9302 | 0.5735 |

## 🏆 Best Model: SVM with Threshold Optimization

The **Support Vector Machine (SVM)** was chosen as the lead model. However, the default decision threshold ($0.5$) yielded a low recall for potable water.

### Precision-Recall Curve Tuning

To maximize the utility of the model, we optimized the decision threshold using the **Precision-Recall Curve**.

* **Optimized Threshold**: `0.3959`
* **Improved F1-Score**: **0.6556**

### Final Performance (Post-Optimization)

After applying the optimized threshold, the model achieved a significantly more balanced performance across both classes:

| Class | Precision | Recall | F1-Score | Support |
| --- | --- | --- | --- | --- |
| **0 (Not Potable)** | 0.75 | 0.69 | 0.72 | 231 |
| **1 (Potable)** | 0.62 | **0.69** | **0.65** | 172 |
| **Accuracy** |  | **0.69** |  | **403** |

**Observation**: By lowering the threshold, we improved the **Recall for Potable Water from 37% to 69%**, ensuring fewer safe water sources are missed while maintaining a global accuracy of 69%.

## 🚀 Impact & Perspectives

1. **Public Health**: Correctly flagging 69% of potable water while maintaining high precision for hazards.
2. **Model Stability**: The weighted average metrics (0.69) demonstrate the model's reliability on unseen data.
3. **Future Work**: Integration of **SHAP** values for chemical explainability and **SMOTE** for further class balancing.
