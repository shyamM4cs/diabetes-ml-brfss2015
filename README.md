# Diabetes ML — BRFSS 2015

An end-to-end 3-class machine learning prediction system for distinguishing **no diabetes, prediabetes, and diabetes** using 253,680 BRFSS 2015 health records.

The project focuses not only on overall predictive performance, but also on **class imbalance, minority-class identification, feature engineering, model comparison, cross-validation, hyperparameter tuning, and the limitations of predicting prediabetes from health and lifestyle indicators.**

---

## Project Overview

Diabetes is not a simple binary problem. Before diabetes develops, individuals may fall into a **prediabetes** category, making reliable identification of this intermediate class particularly important.

This project investigates whether machine learning models can distinguish between:

* **0 — No diabetes**
* **1 — Prediabetes**
* **2 — Diabetes**

A major focus of the project is understanding whether apparently strong overall performance actually translates into useful identification of the less-represented classes.

---

## Research Questions

The project was designed around the following questions:

1. Which health, lifestyle, and demographic factors are most strongly associated with diabetes status?
2. What characteristics distinguish prediabetes from no diabetes and diabetes?
3. Can combinations of health and lifestyle variables provide additional predictive information?
4. How do different machine learning algorithms perform on this multiclass problem?
5. How does class imbalance affect model performance?
6. Can feature engineering and model tuning improve predictive performance?
7. What types of classification errors occur, particularly for the minority prediabetes class?

---

## Dataset

The project uses the **Diabetes Health Indicators Dataset derived from the 2015 Behavioral Risk Factor Surveillance System (BRFSS)**.

### Dataset characteristics

* **Records:** 253,680
* **Features:** 21
* **Target:** `Diabetes_012`
* **Problem type:** Multiclass classification

### Target classes

| Class | Meaning                             |
| ----- | ----------------------------------- |
| 0     | No diabetes / only during pregnancy |
| 1     | Prediabetes                         |
| 2     | Diabetes                            |

The dataset is highly imbalanced:

| Class       | Records |
| ----------- | ------: |
| No diabetes | 213,703 |
| Diabetes    |  35,346 |
| Prediabetes |   4,631 |

This imbalance became an important part of the analysis because a model can achieve relatively strong overall accuracy while performing poorly on the minority class.

---

## Machine Learning Workflow

The project follows an end-to-end machine learning workflow:

```text
Data Exploration
      ↓
Data Preprocessing
      ↓
Exploratory Data Analysis
      ↓
Baseline Models
      ↓
Feature Engineering
      ↓
Feature Transformations
      ↓
Feature Selection
      ↓
Cross-Validation
      ↓
Hyperparameter Tuning
      ↓
Final Model Evaluation
      ↓
Error & Minority-Class Analysis
```

---

## Models Evaluated

Several supervised machine learning algorithms were evaluated:

* Logistic Regression
* K-Nearest Neighbors (KNN)
* Decision Tree
* Random Forest

The models were compared using metrics beyond accuracy because of the substantial class imbalance.

---

## Evaluation Metrics

The project evaluates models using:

* Accuracy
* Precision
* Recall
* F1-score
* ROC-AUC
* Class-wise performance
* Confusion matrices
* Cross-validation performance

Particular attention was given to **precision, recall, and F1-score for the prediabetes class**, since this class represents a much smaller portion of the dataset.

---

## Feature Engineering

Feature engineering was used to investigate whether relationships between variables could provide additional predictive information.

Examples included:

* Squared transformations such as `BMI²`
* Interaction features
* Health and lifestyle combinations
* Transformations of selected variables
* Feature selection

For example, an interaction between BMI and physical activity was explored to represent the possibility that the relationship between body mass and diabetes risk may depend on activity level.

The feature-engineering stage improved the Logistic Regression ROC-AUC from the baseline to approximately **0.814**, with further transformations reaching approximately **0.819** before feature selection.

---

## Cross-Validation

Cross-validation was used to evaluate whether model performance was consistent across different subsets of the training data.

A stratified cross-validation strategy was used so that the class distribution was preserved across folds.

The cross-validation ROC-AUC scores were approximately:

```text
0.822
0.823
0.817
0.824
0.818
```

Mean ROC-AUC:

```text
0.821
```

Standard deviation:

```text
0.003
```

The relatively small standard deviation indicates that the evaluated approach produced reasonably consistent performance across the validation folds.

---

## Hyperparameter Tuning

After establishing baseline and feature-engineered models, hyperparameter tuning was performed to investigate whether model configuration could improve generalization.

The tuning process was evaluated using cross-validation rather than relying only on a single train/test split.

The final tuned models were then evaluated on the held-out test set.

---

## Key Findings

### 1. Accuracy does not tell the whole story

The dataset is heavily dominated by the no-diabetes class.

Consequently, a model can achieve relatively high overall accuracy without being effective at identifying the minority classes.

### 2. Prediabetes was particularly difficult to identify

The prediabetes class contained only **4,631 records**, compared with more than 213,000 no-diabetes records.

Baseline Logistic Regression achieved strong overall accuracy, but its classification performance for the prediabetes class was extremely poor.

This demonstrates why evaluating only accuracy would have produced a misleading interpretation of model quality.

### 3. Feature engineering provided additional predictive information

Feature interactions and transformations improved the ROC-AUC of Logistic Regression compared with the initial baseline.

This suggests that some useful predictive relationships are not captured as effectively when the original variables are considered independently.

### 4. Model complexity did not automatically produce better results

More complex tree-based models did not necessarily outperform Logistic Regression on this dataset.

This reinforces the importance of evaluating models empirically rather than assuming that a more complex algorithm will always produce better predictions.

### 5. Prediction is not the same as clinical diagnosis

The model is designed to identify statistical patterns associated with diabetes categories in BRFSS data.

It should **not** be interpreted as a clinical diagnostic system.

---

## Limitations

Several limitations should be considered when interpreting the results:

* The dataset is highly imbalanced.
* Prediabetes is substantially underrepresented.
* BRFSS variables are largely based on survey responses and self-reported information.
* The available features do not represent the full clinical information used for medical diagnosis.
* Predictive performance on this dataset does not guarantee performance on another population or dataset.
* The model should not be used as a substitute for professional medical diagnosis.

---

## Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Scikit-learn
* Jupyter Notebook
* Git
* GitHub

---

## Project Structure

```text
diabetes-ml-brfss2015/
│
├── Diabetes Disease Detection .ipynb
├── README.md
└── .gitignore
```

Additional figures, results, and supporting files can be added as the project documentation is expanded.

---

## Future Improvements

Potential extensions include:

* More advanced imbalance-handling techniques
* Threshold optimization
* More detailed error analysis
* Explainable ML techniques
* Additional model families
* External validation on another dataset
* More systematic analysis of minority-class prediction
* Improved visualization and reporting

---

## Conclusion

This project demonstrates an end-to-end machine learning workflow for a real-world multiclass health prediction problem.

The most important lesson from the analysis is that **a high overall accuracy does not necessarily mean that a model is useful across all classes**.

In particular, the difficulty of identifying prediabetes highlights the importance of class-wise evaluation, appropriate validation strategies, feature engineering, and careful interpretation of machine learning results in health-related datasets.
