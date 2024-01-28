---
layout: post
math: true
toc: true
---
## Linear Regression Overview
Linear regression is a statistical method used to model the linear relationship between a dependent variable y and one or more independent variables $$ x_{1}, x_{2}, \ldots, x_{p} $$. It is simple, yet it remains one of the most useful analytical tools. While it may not always yield the highest accuracy, its interpretability is unparalleled.

The linear regression model takes the form:

$$ y = \beta_{0} + \beta_{1} x_{1} + \beta_{2} x_{2} + \cdots + \beta_{p} x_{p} + \varepsilon $$

where:

- y is the dependent variable
- $$ x_1, x_2, \ldots, x_p $$ are the independent variables
- $$ \beta_0, \beta_1, \ldots, \beta_p $$ are the coefficients (parameters) of the model
- $$ \varepsilon $$ is the error term, which represents the difference between the observed and predicted values of y.

Often these $n$ equations are stacked together and written in matrix notation as:

$$ \mathbf{y} = \mathbf{X} \mathbf{\beta} + \mathbf{\varepsilon} $$

where:

$$
\mathbf{y} = \begin{pmatrix} y_1 \\ y_2 \\ \vdots \\ y_n \end{pmatrix}, \quad 
\mathbf{X} = \begin{pmatrix} 
    \mathbf{x}_1^\mathsf{T} \\ 
    \mathbf{x}_2^\mathsf{T} \\ 
    \vdots \\ 
    \mathbf{x}_n^\mathsf{T} 
\end{pmatrix} = \begin{pmatrix} 
    1 & x_{11} & \cdots & x_{1p} \\ 
    1 & x_{21} & \cdots & x_{2p} \\ 
    \vdots & \vdots & \ddots & \vdots \\ 
    1 & x_{n1} & \cdots & x_{np} 
\end{pmatrix}
$$

$$
\mathbf{\beta} = \begin{pmatrix} \beta_0 \\ \beta_1 \\ \beta_2 \\ \vdots \\ \beta_p \end{pmatrix}, \quad 
\mathbf{\varepsilon} = \begin{pmatrix} \varepsilon_1 \\ \varepsilon_2 \\ \vdots \\ \varepsilon_n \end{pmatrix}
$$

### Least Square Estimation

Least square error tries to minimize the sum of square residuals: $$ \varepsilon = \sum(y-\hat{y})^2 $$.

To minimize this $$ \varepsilon $$:

$$
\begin{align*}
E &= \sum(\hat{y} - y)^2 \\
&= \lVert \hat{y} - y \rVert_2^2 \\
&= \lVert Xw - y \rVert_2^2 \\
&= (Xw-y)^T(Xw-y) \\
&= ((Xw)^T - y^T)(Xw - y) \\
&= (w^TX^TXw^T - 2w^TX^Ty + y^Ty)
\end{align*}
$$

$$ 	\nabla E = 2(X^TXw - X^T y) = 0 $$

$$ \Rightarrow X^TXw = X^Ty $$

$$ \Rightarrow w_{optimial} = (X^TX)^{-1}X^T y $$

where $$ X^TX $$ is invertible.


It's known that $$ x_{1}, x_{2}, \ldots, x_{p} $$ need to be independent of each other for the matrix $X$ to be invertible. In practice, we often assume that variables are independent from each other, even if they exhibit small correlations. However, if variables are strongly correlated (dependent), they shouldn't be included in the linear model, as they will lead to incorrect results. 

There are several methods to handle multiple dependent variables in regression models:

- Variable selection based on criteria such as Bayesian Information Criterion (BIC) or Akaike Information Criterion (AIC).
- Regularization techniques such as Ridge regression, Lasso regression, and Elastic Net regression, which penalize the inclusion of multiple correlated variables in the model.

These methods help address the issue of multicollinearity and improve the accuracy and reliability of the regression model.

### Maximum Likilihood Estimation 

\begin{align*}
f(y_i | x_i, \beta_0, \beta_1, \ldots, \beta_p) &= \\
&\frac{1}{\sqrt{2 \pi \sigma^2}} \exp\left(-\frac{(y_i - (\beta_0 + \beta_1 x_{i1} + \beta_2 x_{i2} + \cdots + \beta_p x_{ip}))^2}{2\sigma^2}\right)
\end{align*}

The likelihood function for the entire dataset $$\{(x_i, y_i)\}_{i=1}^n $$ is the product of the likelihoods of individual observations:

$$
L(\beta_0, \beta_1, \ldots, \beta_p) = \prod_{i=1}^n f(y_i | x_i, \beta_0, \beta_1, \ldots, \beta_p)
$$

$$
\ell(\beta_0, \beta_1, \ldots, \beta_p) = \log L(\beta_0, \beta_1, \ldots, \beta_p)
$$


$$
\frac{\partial \ell}{\partial \beta_j} = 0, \quad \text{for } j = 0, 1, \ldots, p
$$

Solving this system of equations gives us the maximum likelihood estimates $$ \hat{\beta}_0, \hat{\beta}_1, \ldots, \hat{\beta}_p $$.

This approach provides estimates that maximize the likelihood of observing the given data under the assumed linear regression model. When $$f_θ$$ is a normal distribution with zero mean and variance θ, the resulting estimate is identical to the least square estimation.

### Other Estimation Technique (quantile regression)
Other estimation techniques like quantile regression are also very useful. It focuses on the conditional quantiles of y given X rather than the conditional mean of y given X. Least square estimation is highly affected by outliers, but quantile regression is more robust to outliers. Quantile regression is very useful in some real-world data with outliers. 

### Convexity
A good error function is required to be convex, which has only one minimum point. This property simplifies the optimization process, as there is no risk of getting stuck in a suboptimal solution. Mathematicians/Statisticians put much effort into designing a convex error function. 
In addition, the least square error is the quadratic objective function, while the quantile error function is the linear objective function. In terms of efficiency, linear objective function like quantile regression runs much faster than least-squared regression in large datasets. 
