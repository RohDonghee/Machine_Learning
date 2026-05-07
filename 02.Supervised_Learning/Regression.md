# Regression

## Multiple Linear Regression & Core Concepts
Regression is a supervised learning task aimed at predicting a continuous variable using a set of independent variables.

*   **Linear Relationship Assumption:** Multiple linear regression assumes a linear relationship between a continuous response variable ($y$) and multiple continuous explanatory variables ($x$).
*   **Mathematical Model:** The relationship is approximated as a linear combination: $y \approx \hat{y} = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \dots + \beta_p x_p$.
*   **Variable Terminology:**
    *   **$y$ (Target):** Dependent, response, output, or predicted variable.
    *   **$x$ (Inputs):** Independent, predictor, or explanatory variables.
*   **Residual ($\epsilon$):** The difference between the true observed value ($y$) and the predicted value ($\hat{y}$). Formula: $\epsilon = y - \hat{y}$.
*   **Ordinary Least Squares (OLS):** The standard training methodology used to find the optimal parameters ($\beta$) by minimizing the Sum of Squared Errors (SSE).
<p>※ OLS is the fundamental mathematical optimization algorithm used to train standard linear regression models. Its goal is to draw the "best-fitting line" through your data points

## Two Different Scopes of Regression
Regression models use the same mathematical foundation but can be categorized based on the primary objective of the analysis.

| Feature | Explanatory Regression | Predictive Regression |
| :--- | :--- | :--- |
| **Primary Task** | Explain the relationship between explanatory variables and the response variable. | Predict target values in unobserved data using explanatory variables. |
| **Model Goal** | Understand the contribution, direction, and impact of each explanatory variable. | Maximize predictive accuracy on unseen data. |
| **Evaluation Metrics** | Goodness-of-fit ($R^2$), residual analysis, p-values. | Prediction accuracy indicators (MSE, RMSE, MAE, MAPE). |

## Data Partitioning & Error Types
To properly evaluate a regression model, the dataset must be partitioned, and different types of errors must be understood.

*   **Training vs. Test Set:** The total data is divided into a training set and a test set. The fundamental rule is to *never use the test set while training the model*.
*   **Generalization Error:** The expected error of a model over a random selection of records from the true population distribution. Since the true population is unknown, this error cannot be directly computed.
*   **Test Error:** The error evaluated on the unseen test set. It is used as a practical estimate for the generalization error.
*   **Training Error:** The error evaluated on the training set. It typically decreases continuously as model complexity increases.

## Performance Evaluation Measures
Various quantitative metrics are used to measure prediction accuracy and the model's explanatory power.
※ The choice of evaluation metric heavily depends on the specific situation and the business context. There is no single "perfect" metric; instead, you choose the one that aligns best with what you care about most in your predictions
| Metric | Formula / Description | Key Characteristics |
| :--- | :--- | :--- |
| **MSE (Mean Squared Error)** | $\frac{1}{n} \sum e_i^2$ | Heavily penalizes larger errors due to the squaring of residuals. |
| **RMSE (Root Mean Squared Error)** | $\sqrt{MSE}$ | Returns the error metric to the same scale as the original response variable. It is the most widely used metric. |
| **MAE (Mean Absolute Error)** | $\frac{1}{n} \sum \|e_i\|$ | Treats all errors proportionally without exaggerating large errors. |
| **MAPE (Mean Absolute Percentage Error)** | $\frac{100\%}{n} \sum \|\frac{e_i}{y_i}\|$ | Represents the error as a percentage, making it easy to interpret across different scales. |
| **$R^2$ (Coefficient of Determination)** | $1 - \frac{SSE}{SST} = \frac{SSR}{SST}$ | Goodness-of-fit measure ($0 \le R^2 \le 1$). Represents the proportion of variance in $y$ explained by the linear model. |

## Model Complexity: Underfitting & Overfitting
The complexity of a linear regression model is largely defined by the number of independent variables (parameters) included.

*   **Underfitting:** Occurs when a model is too simple to capture the underlying pattern of the data. Both training and test errors remain high.
*   **Overfitting:** Occurs when a model becomes overly complex and starts fitting the noise in the training data rather than the true signal.
*   **The Trade-off:** As model complexity increases, the training error continues to decrease toward zero. However, the test error eventually starts to increase, indicating the onset of overfitting. More complex models are not always better (Ockham's Razor).

## Sparse Regression & Regularization
Ordinary Least Squares (OLS) estimates often have low bias but large variance, making them prone to overfitting, especially with many predictors. Sparse regression techniques address this by reducing complexity.

*   **Subset Selection:** Finding a parsimonious model by selecting only a small, highly effective subset of the independent variables.
    *   **Forward-Stepwise Selection:** Starts with a null model and sequentially adds the predictor that most improves the model fit (largest $R^2$ increase) until a threshold is met.
    *   **Backward-Stepwise Selection:** Starts with the full model containing all variables and sequentially deletes the predictor that has the least impact on the fit.
*   **Regularization:** Discourages extreme parameter values to prevent overfitting by adding a penalty term to the OLS objective: $\min (\text{Total Error} + C \times \text{Penalty}(\beta))$.
    *   **Hyperparameter $C$:** Controls the weight of the regularization. A larger $C$ penalizes large weights more heavily, focusing heavily on avoiding overfitting.

| Regularization Type | Penalty Term | Characteristics |
| :--- | :--- | :--- |
| **Lasso (L1)** | $C \sum \|\beta_i\|$ (L1 Norm) | Uses absolute values for the penalty. It can shrink some parameter coefficients exactly to zero, effectively performing automatic feature selection. |
| **Ridge (L2)** | $C \sum \beta_i^2$ (L2 Norm) | Uses squared values for the penalty. It shrinks coefficients close to zero to reduce variance, but rarely forces them to exactly zero. |

## Interpretation of Regression Results
Extracting meaningful insights from the trained model is a critical phase of the regression process.

*   **Coefficient Sign (+/-):** Determines the direction of the relationship. A positive sign indicates that as the independent variable increases, the dependent variable also increases.
*   **Coefficient Magnitude:** A larger absolute coefficient suggests that the corresponding variable has a more significant impact on the dependent variable.
*   **Crucial Condition (Normalization):** You can **only** compare the magnitudes of regression coefficients to determine variable importance if the data has been **normalized or standardized** prior to training. Without matching scales, comparing coefficients is mathematically meaningless.
