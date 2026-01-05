# Predictive Modeling of Housing Prices in Boston Using Machine Learning Techniques

## Key Takeaways
## Task-1: Data Preprocessing & EDA 

* Dataset loaded from an external source due to ethical concerns (racially sensitive feature).
* No missing values; already mostly preprocessed.
* Small dataset (506 rows, 14 features) — limits model generalizability.
* CHAS and RAD are categorical but stored numerically; no one-hot encoding needed.
* Significant outliers in CRIM, ZN, and B — not removed due to dataset size.
* StandardScaler used for feature scaling to handle feature variance while retaining outliers.

**Limitations:** Small size, ethical concerns, and presence of outliers.</br>
**Importance:** Clean and simple dataset for learning regression basics.

## Task-2: Train & Evaluate Regression Models

* **Without CV:**
  * **Best:** Random Forest (R²: 0.89)
  * **Worst:** SVM & Linear Regression (R² ≈ 0.65)

* **With GridSearchCV:**
  * Random Forest stayed best.
  * SVM improved (R²: 0.83)
  * Decision Tree overfit (R²: 0.73)

* **With RandomizedSearchCV:**
  * All models improved.
  * Decision Tree (R²: 0.86), Random Forest (R²: 0.86), SVM (R²: 0.83)

**Importance:** Random Forest is the most consistent. Hyperparameter tuning boosts performance.
**Limitation:** Small dataset, risk of overfitting, no CV tuning for Linear Regression.

## Task-3: Convert Regression to Classification

* **Target Conversion:**
  * Used **quantiles** to categorize prices into **Low**, **Medium**, and **High**.
  * Applied **LabelEncoder** to map labels numerically.

* **Preprocessing:** Features scaled using **StandardScaler**.

* **Model Training:**

  * Trained **4 classifiers**: Logistic Regression, Decision Tree, Random Forest, and SVM.

**Importance:** Regression labels successfully transformed into classes for classification tasks.

**Limitation:** Quantile-based binning may cause class imbalance; label boundaries are arbitrary.

 ## Task-4: Classification Metrics

* **Best Overall Performance:**
  * **Logistic Regression** achieved highest accuracy (**80.4%**) and strong precision/recall across all classes.

* **Model Comparison (Accuracy):**
  * Logistic Regression: **0.804**
  * Random Forest: **0.735**
  * SVM: **0.725**
  * Decision Tree: **0.686**

* **ROC-AUC (per class):**
  * **Logistic Regression:** 0.92 (Low), 0.98 (Medium), 0.87 (High)
  * **SVM:** 0.92, 0.97, 0.87 (very close to Logistic)
  * Others showed lower scores, especially in class 2

**Importance:** Logistic Regression performed best in classification accuracy and ROC-AUC. SVM was a close second.
**Limitation:** Class 2 ("High") consistently had lower precision and recall across models.

## Task-5: Ensemble Learning & Feature Importance

* **Ensemble Model Performance (Accuracy):** Bagging has the Highest accuracy, Strong f1-scores for High and Low, Performs most consistently across all classes.
* **Decision Tree:**
  * Top feature: **LSTAT**
  * Top 5: LSTAT, RM, CRIM, AGE, INDUS, B

* **Random Forest:**
  * Top features: **RM**, **LSTAT**
  * Others: AGE, DIS, CRIM

* **SVM Feature Weights:**
  * **Positive Impact:** RAD, RM, ZN, INDUS, CHAS
  * **Negative Impact:** All other features

**Importance**
* **RM** and **LSTAT** consistently emerged as the most important features.
* **RAD** shows a strong positive influence in linear models (SVM, Logistic).
* Ensemble methods (Random Forest, Decision Tree) provide stable and interpretable feature rankings.

**Limitation:**
* Feature importance varies by model type.
* SVM weights can be harder to interpret due to scaling.