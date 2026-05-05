# 📊 Customer Churn Prediction using Ensemble Learning

## 🧠 Project Overview

This project focuses on predicting customer churn using machine learning techniques. The objective is to identify customers who are likely to leave a service so that proactive retention strategies can be applied.

The workflow includes:

* Data cleaning and preprocessing
* Exploratory Data Analysis (EDA)
* Model building and evaluation
* Ensemble learning (Voting & Stacking)
* Threshold tuning for optimal decision making
* Model interpretation using permutation importance

---

## 🧹 Data Preprocessing

The dataset was cleaned and prepared using the following steps:

* Converted categorical target variable:

  ```python
  df['Churn'] = df['Churn'].map({'Yes': 1, 'No': 0})
  ```
* Handled missing values in `TotalCharges`
* Converted data types (object → float where required)
* Applied encoding for categorical variables
* Used scaling where necessary (inside pipeline to prevent data leakage)

---

## 📊 Exploratory Data Analysis (EDA)

EDA was performed to understand feature relationships and distributions:

* Churn distribution analysis
* Correlation heatmap
* Feature vs churn comparison (e.g., tenure, monthly charges)
* Identification of key patterns influencing churn

---

## ⚙️ Model Building

Multiple models were trained and compared:

* Logistic Regression
* Random Forest
* K-Nearest Neighbors
* XGBoost

To improve performance, ensemble methods were used:

### 🔹 Voting Classifier

Combines predictions from multiple models using soft voting.

### 🔹 Stacking Classifier

Uses base models and a meta-learner to improve predictions.

---

## 📈 Model Evaluation

Evaluation metric used:

* **ROC-AUC Score**

Results:

* Voting Classifier: **0.8477**
* Stacking Classifier: **0.8480**

### ✅ Key Insight:

Both models performed almost identically. The difference (~0.0003) is negligible and not statistically significant.

---

## 🎯 Final Model Selection

The **Voting Classifier** was selected as the final model because:

* Comparable performance to stacking
* Simpler architecture
* Faster training and inference
* Easier to interpret and explain

---

## 🔧 Threshold Tuning

Instead of using the default threshold (0.5), threshold tuning was performed to optimize classification performance.

### 📊 Results Summary:

| Threshold | Precision | Recall | F1 Score  |
| --------- | --------- | ------ | --------- |
| 0.45      | 0.535     | 0.815  | 0.646     |
| 0.50      | 0.559     | 0.777  | 0.650     |
| 0.55      | 0.600     | 0.727  | **0.657** |
| 0.60      | 0.639     | 0.660  | 0.649     |

---

## ✅ Final Threshold Selection: **0.55**

### 📌 Reasoning:

* Achieves the **highest F1-score (0.657)**
* Provides a **balanced trade-off** between precision and recall
* Maintains good recall (important for churn detection)
* Avoids excessive false positives

### 💼 Business Justification:

In churn prediction:

* Missing a churner (false negative) is costly
* Slightly lower precision is acceptable

Thus, threshold = **0.55** provides an optimal balance.

---

## 🔍 Model Interpretation

SHAP was initially considered but removed due to:

* Incompatibility with ensemble pipelines
* High computational cost
* Increased complexity

### ✅ Alternative Used: Permutation Importance

Permutation importance was used to identify key features affecting predictions:

* Model-agnostic
* Works with ensemble models
* Easy to interpret

---

## 🚀 Key Takeaways

* Ensemble learning improves model robustness
* Voting classifier performs as well as stacking with less complexity
* Threshold tuning significantly improves classification performance
* Model interpretability can be achieved without SHAP

---

## 📌 Conclusion

The final model (Voting Classifier with threshold = 0.55) provides a strong balance between performance and interpretability. This approach ensures effective identification of potential churn customers while maintaining practical usability in real-world applications.

---

## 🛠️ Tech Stack

* Python
* Pandas, NumPy
* Scikit-learn
* Matplotlib, Seaborn

---

## 📬 Author

**Aryan Sonkar**
B.Tech AI & DS
IIITDM Kurnool

---
