# Classification

## Fundamentals of Classification
Classification is a supervised learning task aimed at learning a model that maps an attribute set ($x$) into one of the predefined discrete class labels ($y$).
*   **Objective:** The trained classifier must excel not only on the training data but also generalize well to correctly predict class labels for unseen test data.
*   **Key Algorithms:** Decision Trees, Logistic Regression, Naïve Bayes, K-Nearest Neighbors (KNN), Random Forests, etc.

## Decision Tree
Decision Trees make predictions by recursively splitting the data based on attribute tests.
*   **Hunt’s Algorithm:** A greedy approach where if a node contains mixed classes, an attribute test is selected to split the data into smaller, purer subsets.
*   **Splitting Strategies:** Can be binary (dividing values into two subsets) or multi-way (creating as many partitions as distinct values).

| Impurity Measures & Splitting | Description & Formula |
| :--- | :--- |
| **Entropy** | Measures node impurity. Formula: $-\sum p_i(t) \log_2 p_i(t)$. |
| **Gini Index** | Another measure of node impurity. Formula: $1 - \sum p_i(t)^2$. |
| **Information Gain** | The reduction in impurity achieved by a split. Calculated as the impurity before splitting ($P$) minus the weighted impurity after splitting ($M$). The algorithm greedily chooses the split with the highest Information Gain ($P - M$). |

| Complexity & Pruning | Description |
| :--- | :--- |
| **Overfitting** | Occurs when the tree becomes overly complex (too many nodes); training error is near zero, but generalization (test) error sharply increases. |
| **Pre-pruning** | Halts the tree-growing algorithm early based on specific conditions (e.g., maximum depth reached, insufficient node purity, or too few data points). |
| **Post-pruning** | Grows the tree fully, then trims it in a bottom-up fashion. Sub-trees are replaced by a leaf node if the generalization error improves. |

| Pros | Cons |
| :--- | :--- |
| - Fast training and prediction.<br>- Easy to interpret (IF-THEN rules).<br>- Robust to noise and redundant attributes.<br>- No data normalization required. | - Splits are strictly axis-aligned (single attribute at a time).<br>- The greedy nature may miss crucial interacting attributes. |

## Probabilistic Models: Logistic Regression & Naïve Bayes
Instead of outputting a strict class label, these models estimate the *probability* of an instance belonging to a certain class.

*   **Bayes Theorem:** A probabilistic framework that calculates the posterior probability $P(Y|X)$ based on prior probability, likelihood of evidence, and prior probability of evidence.

| Model | Core Concept & Mechanism | Key Characteristics |
| :--- | :--- | :--- |
| **Logistic Regression** | Models the probability of a class as a function of predictors. It uses the **Logit transformation** ($\log(p/(1-p)) = \beta_0 + \beta_1 X$) to handle probability bounds. | Restores the probability using the **Sigmoid function** ($1 / (1 + e^{-z})$). A cutoff threshold (e.g., $p > 0.5$) is then applied to assign the final class. |
| **Naïve Bayes** | Uses Bayes Theorem under the strong assumption of **Conditional Independence** among all attributes given the class label ($P(X_1, X_2...|Y) = \prod P(X_i|Y)$). | Extremely fast. For continuous variables, data is either discretized into histogram bins or modeled using probability distributions. |

## K-Nearest Neighbors (KNN)
KNN is an instance-based learning method that classifies an unknown record based on its proximity to training records.
*   **Mechanism:** It computes the distance between the test record and all training records, chooses the $K$ "nearest" records, and assigns a class via a majority vote (or distance-weighted vote where weight $w = 1/d^2$).
*   **Normalization:** Data preprocessing (scaling/standardization) is strictly required so that attributes with large numerical ranges (e.g., income) do not dominate the distance metric.
*   **Choosing $K$:** A hyperparameter trade-off. If $K$ is too small, the model is highly sensitive to noise. If $K$ is too large, the neighborhood may mistakenly include points from other classes.

## Performance Evaluation & Metrics
Relying solely on "Accuracy" is misleading in **Class Imbalance** problems (e.g., fraud detection, disease diagnosis), where detecting a very rare positive class is the main objective.

| Metric | Formula | Interpretation |
| :--- | :--- | :--- |
| **Confusion Matrix** | TP, FP, TN, FN | A table tracking True Positives, False Positives (Type I error), True Negatives, and False Negatives (Type II error). |
| **Accuracy** | $\frac{TP+TN}{TP+FN+FP+TN}$ | The proportion of total correct predictions. |
| **Precision** | $\frac{TP}{TP+FP}$ | The proportion of positive predictions that were actually correct. |
| **Recall / Sensitivity (TPR)**| $\frac{TP}{TP+FN}$ | The proportion of actual positive cases successfully detected. |
| **F1 Score** | $2 \times \frac{Precision \times Recall}{Precision + Recall}$ | The harmonic average of precision and recall; highly useful for imbalanced datasets. |
| **Specificity** | $\frac{TN}{FP+TN}$ | How well the model correctly identifies negative cases (avoids false alarms). |

## ROC Curve & Asymmetric Costs
Classifiers that output probabilities require a discrete cutoff value to make a final prediction, which creates a trade-off between detection rates and false alarm rates.

*   **ROC Curve (Receiver Operating Characteristic):** A graphical plot of the True Positive Rate (TPR) against the False Positive Rate (FPR) across all possible threshold cutoff values.
*   **AUC (Area Under Curve):** Measures the entire 2D area underneath the ROC curve. It is a **cutoff-invariant** metric. An AUC of $1.0$ represents an ideal classifier, while $0.5$ represents a random guess. It is highly effective for objectively comparing multiple models.
*   **Asymmetric Misclassification Costs:** In many domains, the cost of an FN (e.g., missing a cancer diagnosis) is astronomically higher than an FP (e.g., a false alarm). **Cost Matrices** are used to assign exact financial or operational costs to misclassifications, enabling the selection of a model that maximizes total business profit rather than mere accuracy.
