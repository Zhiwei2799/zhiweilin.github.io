---
layout: post
math: true
toc: true
---

## Generalized Linear Regression

Generalized linear regression is an extension of ordinary linear regression. The response variable can be categorical, and the distribution of residuals can be non-normal. Here's a summary:

- Response variable in GLR is no longer confined to the class of normal distribution; it only needs to be a member of the linear exponential family of distributions.
- GLR uses a link function where the response mean is linearly related to the predictors.

### Linear Exponential Family of Distribution

Mathematically, a distribution is a member of the linear exponential family of distributions if its probability function can be expressed as:

$$ f(y;\theta,\phi) = \exp\left(\frac{y\theta - b(\theta)}{\phi} + S(y,\phi)\right) $$

where:
- $$ y $$ is the argument of the probability function.
- $$ \theta $$ is the parameter of interest.
- $$ \phi $$ is the scale parameter.
- $$ b(\theta) $$ and $$ S(y,\phi) $$ are functions of $$ \theta $$ and $$ \phi $$, respectively.

For further details, check this [website](https://en.wikipedia.org/wiki/Exponential_family).

### Link Functions

Link functions connect the response distribution's mean to the predictors. It's a monotonic function that links the mean of the response to a linear combination of predictors:

$$ g(\mu) = X\beta $$

where $$ g(\cdot) $$ is the link function, $$ \mu $$ is the response mean, $$ X $$ is the matrix of predictors, and $$ w $$ is the coefficients.

The monotonicity property allows us to invert the link function and estimate the response mean $$\mu$$ as soon as the parameter vector $$\beta$$ has been estimated from the data:

$$
\mu = g^{-1}(\eta) = g^{-1}(\beta_0 + \beta_1 x_1 + \cdots + \beta_p x_p)
$$

### Canonical Link Function

There are many possible link functions connecting response distribution's mean to the linear predictor. One comman choice of the link function is the canonical link, which sets the sysmatic component $$\eta$$ of the model equal to the paramter $$\theta$$. 

$$g(\mu) = \eta = \theta$$
![IMG_2306](https://github.com/zhiweilin27/zhiweilin27.github.io/assets/111717798/13046288-8f30-4c03-90e3-3a7ff9626ab6)


## Logistic Regression

Logistic regression is one of the most famous generalized linear regression techniques.

- For the classification of two classes (e.g., $$ t=1 $$ or $$ t=0 $$), the link function used is the logistic function (sigmoid curve) defined as $$ f(z) = \frac{1}{1+e^{-z}} $$.
- For multiclass classification, there's an extension called the softmax function defined as:

$$ f(z)_i = \frac{e^{z_i}}{\sum_{j=1}^{K} e^{z_j}} \quad \text{for } i = 1, \ldots, K $$

Let's derive the optimal weights that minimize least squares errors.

First, the logistic regression model is represented as:

$$ P(y|x) =
  \begin{cases} 
    h(x) & \text{for } y = +1 \\
    1 - h(x) & \text{for } y = -1
  \end{cases}
$$

where $$ h(x) = \Theta(w^Tx) $$ and $$ \Theta $$ is the logistic function defined as $$ \Theta(s) = \frac{e^{s}}{1+e^{s}} $$.

Thus,

$$ P(y|x) = \Theta(yw^Tx) $$

One reason for choosing the mathematical form $$\Theta(s) = \frac{e^s}{1+e^s}$$ 
is that it leads to this simple expression for $$P(y|x)$$ 

The likelihood for a sample of size $$ N $$ is given by:

$$ L(\beta;\textbf{y},\textbf{X}) = \prod_{n=1}^{N} P(y_n|x_n) $$

Maximizing the likelihood:

$$
\begin{align*}
&\text{Maximize } \prod_{n=1}^{N} P(y_n | x_n) \\
&\Leftrightarrow \ln\left(\prod_{n=1}^{N} P(y_n | x_n)\right) \quad \text{(This is log-likelihood)} \\
&\equiv \max \sum_{n=1}^{N} \ln P(y_n | x_n) \\
&\Leftrightarrow \min -\frac{1}{N} \sum_{n=1}^{N} \ln P(y_n | x_n) \\
&\equiv \frac{1}{N} \sum_{n=1}^{N} \ln\left(\frac{1}{P(y_n | x_n)}\right) \\
&\equiv \frac{1}{N} \sum_{n=1}^{N} \ln\left(\frac{1}{\Theta(y_n w^T x_n)}\right) \\
&\equiv \frac{1}{N} \sum_{n=1}^{N} \ln(1 + e^{-y_n w^T x_n})
\end{align*}
$$

$$ E(w) = \frac{1}{N} \sum_{n=1}^{N} \ln(1 + e^{-y_n w^T x_n}) $$

The first-order derivative of the logistic regression objective function $$ E(w) $$ with respect to the weight vector $$ w $$ is derived as follows:

$$
\begin{align*}
\nabla E(w) &= \nabla\left(\frac{1}{N}\sum_{n=1}^{N}\ln(1+e^{-y_nw^Tx_n})\right) \\
&= \frac{1}{N}\sum_{n=1}^{N}\frac{-y_nx_ne^{-y_nw^Tx_n}}{1+e^{-y_nw^Tx_n}} \\
&= \frac{1}{N}\sum_{n=1}^{N}\frac{-y_nx_ne^{-y_nw^Tx_n}}{1+e^{-y_nw^Tx_n}}\cdot\frac{1+e^{y_nw^Tx_n}}{1+e^{y_nw^Tx_n}} \\
&= \frac{-1}{N}\sum_{n=1}^{N}\frac{y_nx_n(e^{-y_nw^Tx_n}+1)}{(1+e^{-y_nw^Tx_n})(1+e^{y_nw^Tx_n})} \\
&= \frac{-1}{N}\sum_{n=1}^{N}\frac{y_nx_n}{1+e^{y_nw^Tx_n}}
\end{align*}
$$

This concludes the derivation.

### Decision Boundary
The logistic function is used to map the output of a linear combination of features (i.e., the weighted sum of input features plus a bias term) to a probability value between 0 and 1. And since the logistic function(sigmoid function) is a monotonically increasing function - when x increases, y increases, the decision boundary remains linear as in linear regression. 

Proof of Decision Boundary for one-variable when p(y=1|x) = p(y=0|x):\\
$$
\frac{1}{1 + e^{-(\beta_0 + \beta_1 x)}} = \frac{1}{2}
$$\\
$$
2 = 1 + e^{-(\beta_0 + \beta_1 x)}
$$\\
$$
1 = e^{-(\beta_0 + \beta_1 x)}
$$\\
$$
\ln(1) = -(\beta_0 + \beta_1 x)
$$\\
$$
0 = -(\beta_0 + \beta_1 x)
$$\\
$$
0 = \beta_0 + \beta_1 x
$$\\
$$
x = -\frac{\beta_0}{\beta_1}
$$

This can be extended to multi-variables. 


The plot below is an example of a decision boundary for logistic regression:\\
![decision-boundary](https://github.com/zhiweilin27/zhiweilin27.github.io/assets/111717798/ec282923-e57a-47ab-b4e2-b2419c421a51)

## Support Vector Machine
SVM is to find a plane that has the maximum margin, i.e. the maximum distance between data points of both classes. 

![Capture](https://github.com/zhiweilin27/zhiweilin27.github.io/assets/111717798/261f95b1-3d93-426f-8908-81c7152e94c0)

Hinge Loss is the loss function used in Support Vector Machines (SVM). The objective is to find the values of $$ w $$ and $$ b $$ that minimize:
$$
\min_{w, b} \frac{1}{2}||w||^2 + C \sum_{i=1}^{n} \xi_i
$$
Subject to the constraints:
$$
y_i(w \cdot x_i + b) \geq 1 - \xi_i, \quad \forall i = 1, \ldots, n
$$
$$
\xi_i \geq 0, \quad \forall i = 1, \ldots, n
$$

Kernel Tricks: The kernel function computes the inner product between two vectors 
- **Linear Kernel:** The simplest form, where the kernel is just the dot product of two vectors. It is used when the data is linearly separable.
  $$
  K(x, x') = x \cdot x'
  $$

- **Polynomial Kernel:** Allows learning of non-linear models by mapping inputs into polynomial feature space.
  $$
  K(x, x') = (\gamma x \cdot x' + r)^d
  $$

- **Radial Basis Function (RBF) or Gaussian Kernel:** One of the most common kernels. It can map the inputs into an infinite-dimensional space, providing great flexibility in fitting the data.
  $$
  K(x, x') = \exp(-\gamma \|x - x'\|^2)
  $$

### Decision Boundary
The decision boundary of an SVM is determined by the choice of the kernel: 
- Linear Kernel: The decision boundary is linear.
- Non-linear Kernels (Polynomial and RBF): The decision boundary is non-linear

An example of an RBF decision boundary is:
![Capture](https://github.com/zhiweilin27/zhiweilin27.github.io/assets/111717798/99f9e3bf-ab9a-4cc4-bd23-3b5b2aa8a88f)



