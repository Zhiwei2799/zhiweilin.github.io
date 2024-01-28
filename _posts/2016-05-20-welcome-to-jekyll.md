---
layout: post
math: true
toc: true
---
## Linear Regression 
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

## Least Square Error

Least square error tries to minimize the sum of square residuals: $$ \varepsilon = \sum(y-\hat{y})^2 $$.

To minimize this $\varepsilon$:

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

$$ \Rightarrow w = (X^TX)^{-1}X^T y $$

where $$ X^TX $$ is invertible.
