---
layout: post
math: true
toc: true
---
## Multicollinearity 

Multicollinearity occurs when two or more predictors in a regression model are moderately or highly correlated with each other. In the least squares estimation, 

$$ w = (X^TX)^{-1}X^T y $$

Thus, when collinearity is present, coefficient estimates ($$ w $$) for the correlated variables become unstable (X is not invertible).

Several methods address the multicollinearity problem:

- Step-wise regression (variable selection using adjusted $$ R^2 $$, AIC, BIC, or Mallow's $$ C_p $$).
- Shrinkage methods (Ridge, Lasso, or Elastic Net).

## Step-Wise Regression (Variable Selection)

Stepwise regression selects a subset of predictor variables based on statistical criteria such as adjusted $ R^2 $, AIC, BIC, or Mallow's $$ C_p $$.

### Adjusted $$ R^2 $$

The coefficient of determination $$ R^2 $$ is defined as $$ R^2 = 1- \frac{RSS}{TSS} $$. However, as more predictors are added, $$ R^2 $$ always increases. To address this, statisticians developed adjusted $$ R^2 $$, which rescales $$ R^2 $$ to account for the number of predictors.

### AIC, BIC, and Mallow's $$ C_p $$

These model comparison statistics penalize complex models to favor simplicity, following the parsimony principle.

$$
\begin{align*}
\text{Mallow's } C_p & : \frac{RSS+2ps_{\text{full}}^2}{n} \\
\text{AIC} & : 2p-2ln(L) \\
\text{BIC} & : ln(n)p-2ln(L)
\end{align*}
$$

Here, $$ p $$ is the number of predictors, $$ s_{\text{full}}^2 $$ is the mean squared error of the full model, $$L$$ maximum value of the likelihood function for the model.

## Shrinkage Methods

Shrinkage methods regulate or shrink coefficient estimates towards zero.

### Ridge Regression

In Ridge regression, the objective function is:

$$
E(w) = \sum(y_i - (w_0 + w_1x_{i1} + \ldots + w_p x_{ip}))^2 + \lambda \sum (w_j^2),
$$

where $\lambda \geq 0$ is called the tuning parameter. The lambda value is a hyperparameter that needs to be tuned (using cross-validation) to obtain the value of lambda such that the error (RSS) is minimized.




Derive optimal w using matrix annotation: 
$$ E(w) = ||xw-t||^2+\lambda ||w||^2 $$

$$ \nabla E(w) = 2x^Txw - 2x^Ty+ 2 \lambda w =0 $$

$$ \Rightarrow 2x^Txw + 2\lambda w = 2x^T y $$

$$ w = \frac{x^Ty}{x^Tx+\lambda I} $$

$$ \Rightarrow w = (x^Tx + \lambda I)^{-1}(x^Ty) $$

### Lasso Regression

In Lasso regression, the objective function is similar to Ridge, but the penalty term involves the absolute value of the coefficients:

$$
E(w) = \sum(y_i - (w_0 + w_1x_{i1} + \ldots + w_p x_{ip}))^2 + \lambda \sum (|w_j|).
$$

In contrast to Ridge regression, the Lasso has the remarkable effect of shrinking the coefficient estimates to be exactly zeros. Therefore, Lasso can also be used for variable selection.



### Elastic Net
Elastic Net combines the penalties of both Lasso and Ridge regression techniques:

$$
E(w) = \sum(y_i - (w_0 + w_1x_{i1} + \ldots + w_p x_{ip}))^2 + \lambda_1 \sum (w_j^2) + \lambda_2 \sum (|w_j|).
$$

Overall, these methods provide effective ways to handle multicollinearity in regression models.

