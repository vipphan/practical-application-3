## Notebook

https://github.com/vipphan/practical-application-3/blob/main/prompt_III.ipynb
## Tools & Libraries used
• Python 

• Pandas 

• NumPy

• Matplotlib

• Seaborn 

• Scikit-learn

## Overview
This project compares the performance of four classification models (K-Nearest Neighbors, Logistic Regression, Decision Trees, and Support Vector Machines) on a dataset of 41,188 phone-based marketing contacts from a Portuguese banking institution (sourced from the UCI Machine Learning Repository). The goal is to predict, before a call is made, whether a client is likely to subscribe to a term deposit, so the bank can prioritize outreach toward the clients most likely to subscribe rather than contacting everyone equally.

The analysis follows the CRISP-DM framework: Business Understanding → Data Understanding → Data Preparation → Modeling → Evaluation → Deployment.

## Approach
**Data cleaning:**
Identified "unknown" as a missing-value encoding across several categorical columns, recoded the `pdays` placeholder value (999) and added a `was_contacted_before` flag, ordinally encoded `education`, and one-hot encoded the remaining nominal categorical features. Excluded `duration` from all models, since it is only known after a call takes place and would leak the outcome.

**EDA:**
Visualized the class imbalance in the target variable, the client age distribution, and the breakdown of job type, marital status, and education level across the client base.

**Modeling:**
Built and compared four classifiers, first using only basic client demographic features, then using the full feature set including campaign history and economic indicators:

* K-Nearest Neighbors
* Logistic Regression
* Decision Tree
* Support Vector Machine

Each model was evaluated at default settings and again after hyperparameter tuning via GridSearchCV.

**Evaluation:**
Compared models using accuracy against a majority-class baseline (0.8876), with an emphasis on both predictive performance and training efficiency given the practical goal of usability at scale.

## Key Findings

* Client demographics alone (age, job, marital status, education, loan status) are not enough to beat the baseline. All four models trained only on bank client features landed at or below 88.76% accuracy.
* Campaign history and economic context features are what actually drive performance. Once added, all four models cleared the baseline meaningfully, with the best models reaching around 90.1% accuracy.
* Logistic Regression offers the best trade-off between accuracy and efficiency, tying for the top test accuracy while training in a few seconds, compared to SVM's 900+ seconds for a comparable result.
* Economic conditions are the strongest predictors. Higher employment variation pushed clients toward not subscribing, while higher interest rates and prices pushed toward subscribing, likely reflecting the relative attractiveness of term deposits under different conditions.
* Contact method and frequency matter. Cellular contact outperformed telephone, and repeated contact attempts within the same campaign were associated with lower, not higher, success.

## Next Steps

* **Test alternative evaluation metrics:** Accuracy is limited by the class imbalance in this dataset. Precision, recall, or F1 score on the "yes" class would give a clearer picture of how well a model identifies actual subscribers.
* **Expand SVM's hyperparameter search:** SVM's grid was kept narrow here due to long training times. A wider search, or testing alternative kernels, could reveal whether its performance can improve further.
* **Validate on more recent campaign data:** Given how strongly economic indicators drove the model's predictions, testing on more recent data would help confirm whether these patterns still hold under current economic conditions.
