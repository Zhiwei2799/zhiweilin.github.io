---
layout: post
math: true
toc: true
---
## Multcollinearity 
Multicollinearity exists when two or more of the predictors (independent variables) in a regression model are moderately or highly correlated with one another. In least square estimation, $$ w = (X^TX)^{-1}X^T y $$. Hence when collinearity is present, coefficient estimates(w) for the correlated variables become unstable (in terms of linear algebra, X is not invertible). 
There are several methods to handle the multicollinearity problem:
- Step-wise regression (variable selection using adjusted $R^2$, AIC, BIC, or Mallow's $$C_p$$)
- Shrinkage methods (ridge, lasso, or elastic net)
## Step-Wise regression (variable selections)
Stepwise regression is a statistical method used to select a subset of predictor variables for a regression model. It can either be going forward or backward that sequentially add or remove predictors based on statistical criteria such as adjusted $R^2$, AIC, BIC, or Mallow's $$C_p$$
### adjusted R^2
The coefficient of determination $$R^2$$ is defined as $$R^2 = 1- \frac{RSS}{TSS}$$. I view this as a percentage variance being captured by the model. high means good, and low means bad. However, as we add more predictors to a linear model, the RSS will always decrease, and therefore $$R^2$$ will always increase. Therefore it wouldn't tell us much about whether the new predictor is good or bad since $$R^2$$ is always increasing.  

Therefore, statisticians have devised a variant of $$R^2$$ known as the $$\mathbf{adjusted R^2}. adjusted R^2 = 1 - (RSS)/(n-p-1)/(TSS/(n-1)) = 1- s^2/ s_y^2. This simply rescales the ordinary R^2 by dividing RSS and TSS by their respective degree of freedom. The reason for doing this is now the adjusted R^2 does not always increase as a new predictor is added in. 

### AIC, BIC, and Mallow's $$C_p$$
These three model comparison statistics all have the following structure in common:
$$ 1/n (RSS + penalty term) $$
Basically, we add more penalties to a more complex model. We want the final model to be simple while efficient. This often refers as the parsimony principle - a simpler model with fewer parameters is favored over more complex models with more parameters.

- Mallow's $$C_p$$: (RSS+2ps_{full}^2)/n
- AIC = 1/n (RSS + 2 ps_{full}^2)
- BIC = 1/n (RSS + ln(n) ps_{full}^2)
  where p is the number of precitors and s_{full}^2 is the MSE of the full model. 
As can be seen, BIC imposes a heavier penalty per parameter than AIC with a large dataset.

## Shrinkage Methods
Instead of going through all possible subset models, the shrinkage method regulates or shrinks the coefficient estimates towards zeros.
### Ridge Regression
In least square regression RSS = \sum(y_i-y_i\hat)^2 = \sum(y_i - (\beta_0 + \beta_1x_{i1}+ .... + beta_p x_{ip}))^2 + \lambda \sum (\beta_j^2). where \lambda >= 0, which is called the tuning parameter. lambda value is hyperparamte, we need to tune it (using cross-validation) to get value of lambda such that the error (RSS) is the lowest. 

use matrix annotation: 
$E_2(w) = ||xw-t||^2+\lambda ||w||^2$ \\
      $ = (xw-y)^T(xw-y) + \lambda w^Tw $ \\
      $ =((xw)^T-y^T)(xw-y)+\lambda w^Tw $\\
      $ =(w^Tx^T-y^T)(xw-y)+\lambda w^Tw  $\\ 
$ =w^Tx^Txw - 2w^Tx^Ty + y^Ty + \lambda w^Tw $ \\

$\nabla E_2(w) = 2x^Txw - 2x^Ty+ 2 \lambda w =0$\\
$\xrightarrow 2x^Txw + 2\lambda w = 2x^T y $ \\
                               $w =\frac{x^Ty}{x^Tx+\lambda I}$ \\ 
                               $  =(x^Tx + \lambda I)^{-1}(x^Ty)$
optimal w = (x^Tx + \lambda I)^{-1}(x^Ty).

### Lasso Regression
In lasso regression, we minimize RSS = \sum(y_i-y_i\hat)^2 = \sum(y_i - (\beta_0 + \beta_1x_{i1}+ .... + beta_p x_{ip}))^2 + \lambda \sum (abs{\beta_j}), where the shrinkage penalty involves the absolute value of the coefficients. 
In contrast to ridge regression, the lasso has the remarkable effect of shrinking the coefficient estimates to be exactly zeros. 

### Elastic Net
It combines the penalties of both Lasso (L1 regularization) and Ridge (L2 regularization) regression techniques. We minimize  RSS = \sum(y_i-y_i\hat)^2 = \sum(y_i - (\beta_0 + \beta_1x_{i1}+ .... + beta_p x_{ip}))^2 + \lambda_1 \sum (\beta_j^2) + \lambda_2\sum (abs{\beta_j}). 
