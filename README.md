# 🧠 Psychological Drivers of Climate Communication: A Supervised Learning Study

## 🚀 Overview
This repository contains the complete code and documentation for a **Supervised Learning Study** investigating the psychological drivers behind the willingness to **share climate-related social media content**.

The project, conducted on behalf of the **GreenVoice Alliance**, aims to develop an efficient binary classification model to support data-driven outreach campaigns. By focusing exclusively on **individual-level psychological features** (beliefs, identity, motivation), the model isolates key levers for targeted communication strategies, moving beyond demographic or country-level variables.

---

## ✨ Value and Goal

### 🎯 Core Objective
Develop a robust binary classification model (Sharer vs. Non-Sharer) to predict the likelihood of an individual sharing a climate post, based solely on psychological predictors.

### 💡 Generated Value
* **Targeted Outreach:** Improves the **efficiency** of online climate campaigns by identifying individuals likely to amplify messages, optimizing resource allocation.
* **Actionable Insights:** Pinpoints the most influential psychological factors (**Environmental Identity** and **Extrinsic Motivation** are key drivers), informing the design of tailored, high-impact messaging.
* **Generalizable Model:** Provides an explanatory framework focusing on modifiable psychological traits, supporting equitable and globally applicable communication strategies.

---

## 💻 Methodology and Results

### 📊 Data Source
The study utilizes cross-national survey data from the recent publication:
> Todorova et al. (2025). *"Machine learning identifies key individual and nation-level factors predicting climate-relevant beliefs and behaviors."* (CC BY 4.0)

The final dataset uses 9 psychological features (e.g., `envid`, `trustsci`, `intmotiv`) and the binary target variable `ccshare` (Willingness to Share). The dataset is relatively balanced (Sharers: 53.4% | Non-Sharers: 46.6%).

### 🛠️ Model Selection & Evaluation
The project implemented a rigorous workflow using:
1.  **Imputation:** Mean imputation for missing values (all $< 5\%$).
2.  **Scaling:** Standard scaling applied conditionally (for k-NN).
3.  **Cross-Validation:** **Nested Cross-Validation** (10 outer folds, 5 inner folds repeated 3 times) for unbiased performance estimation and hyperparameter tuning.
4.  **Metrics:** **F1 Score** (primary optimization metric) and **ROC AUC** (global discriminatory power).

| Model | Setup | F1 Score (Mean) | ROC AUC (Mean) | Fit Time (s) |
| :--- | :--- | :--- | :--- | :--- |
| **Random Forest (Final Model)** | **Nested CV** | **0.717** | **0.765** | 989.6 (Avg. per fold) |
| k-Nearest Neighbors | Nested CV | 0.690 | 0.728 | 49.352 (Avg. per fold) |
| Dummy Classifier (Baseline) | Nested CV | 0.697 | 0.500 | 0.374 (Avg. per fold) |

The **Random Forest Classifier** consistently provided the best balance of prediction accuracy (F1) and class separation (ROC AUC) and was selected as the final model.

### 🔑 Key Findings (Feature Importance)
Permutation importance analysis revealed the hierarchy of psychological drivers based on their predictive power:

* **Most Influential:** **`envid`** (Environmental Identity) and **`extmotiv`** (Extrinsic Motivation).
* **Moderately Influential:** **`scicons`** (Scientific Consensus), **`govtrust`** (Trust in Government), and **`ownestim`** (Personal Impact Estimate).
* **Least Influential:** **`intmotiv`** (Internal Motivation) and **`humanid`** (Humanitarian Identity).

A subsequent **Ablation Study** confirmed the robustness of the model, showing that the removal of low-importance features (`humanid`, `intmotiv`) did not negatively impact the final model performance, validating the choice to focus on core psychological constructs.

---

## ⚙️ Repository Structure
* `notebooks/`: Contains the MADS-ML lecture notebooks and the main project notebook outlining the full methodology and analysis.
* `data/`: Placeholder for the `share.csv` dataset (not included in this public repo, source cited below).
* `src/`: Contains any helper functions, pipelines, or custom classes (e.g., `FeatureDropper`).

---

## 📚 Dependencies
The project was developed using the following core libraries (full list in the project notebook):
* `pandas`
* `numpy`
* `scikit-learn` (Primary ML library)
* `matplotlib`
* `seaborn`
* `time`

---

## ✍️ Data Scientist & Credits
| Attribute | Detail |
| :--- | :--- |
| **Data Scientist** | Maximilian Thiel |
| **Company** | GreenVoice Alliance |
| **Date** | 30.06.2025 |

### 📄 Sources and References
* **Dataset:** Todorova, A. et al. (2025). *"Machine learning identifies key individual and nation-level factors predicting climate-relevant beliefs and behaviors."*
* **Textbooks:** Müller, A. C., & Guido, S. (2016). *Introduction to machine learning with Python*. | James, G. et al. (2023). *An Introduction to Statistical Learning with Applications in Python*.
* **Interpretability:** Molnar, C. *Interpretable Machine Learning: A Guide for Making Black Box Models Explainable.*
* **Documentation:** Scikit-learn documentations and User Guide.

---

## 🛠️ Future Work

1.  **Advanced Algorithms:** Explore Gradient Boosting methods (XGBoost, LightGBM) for potential performance gains in modeling non-linear interactions.
2.  **Behavioral Validation:** Augment the target variable with **real-world observed sharing behavior** (digital trace data) to improve ecological validity.
3.  **Model Explainability:** Incorporate **SHAP values** or **Partial Dependence Plots** for finer-grained, local interpretability of feature effects.
4.  **Intervention Studies:** Design field experiments to test the causal effect of strengthening key predictors (Environmental Identity, Extrinsic Motivation) on actual sharing behavior.