---
layout: post
math: true
toc: true
---

## Principal Components Overview

Suppose we have $$ X $$ as a vector of $$p $$ random variables, then the covariance matrix $$ V$$ is $$ p \times p $$. 
We want to find a vector $$ \alpha_1 = (\alpha_{11}, \alpha_{12}, ..., \alpha_{1p}) $$ such that $$ \alpha_{1}^{T} X $$ gives maximum variance.

In mathematical terms, it is expressed as:

$$
\begin{align*}
\max(\text{cov}(\alpha_{1}^{T} X)) &= \max(\alpha_{1}^{T} X \alpha_{1}) \text{        such that } ||\alpha_{1}||^2 = 1 \\
&\Rightarrow L(\alpha_1, \lambda) = \alpha_{1}^{T} X \alpha_1 - \lambda(||\alpha_{1}||^2 - 1)
\end{align*}
$$

Taking derivatives with respect to $$\lambda $$ and $$\alpha_1$$:

$$
\frac{\delta L}{\delta \lambda} = ||\alpha_{1}||^2 - 1 = 0 
$$

$$
\frac{\delta L}{\delta \alpha_1} = 2(V\alpha_{1}- \lambda \alpha_{1}) = 0 
$$

$$
\Rightarrow V\alpha_{1} = \lambda \alpha_{1}
$$

Therefore, the maximum value for $$ ||\alpha_1||^2 = 1 $$ is $$ \lambda_1 $$. 
Thus, a vector $$ \alpha_1 $$ that gives maximum variance corresponds to the eigenvector for $$ \lambda_1 $$.

For the second vector $$ \alpha_2 $$, it is also required to be uncorrelated with $$ \alpha_1 $$:

$$
\max(\text{cov}(\alpha_{2}^{T} X)) = \max(\alpha_{2}^{T} X \alpha_2) \text{        such that } ||\alpha_2||^2 = 1 \text{ and } \alpha_{1}^{T} \alpha_2 = 0 
$$

$$
\Rightarrow L(\alpha_2, \lambda, \lambda_2) = \alpha_{2}^{T} X \alpha_2 - \lambda(||\alpha_{2}||^2 - 1) - \lambda_2(\alpha_{1}^{T} \alpha_2)
$$

Continues this procedure will find all $$\lambda_k$$, $$\alpha_k$$ for kth P.C. 


Given $$ X $$ is a vector of $$ P $$ and the covariance matrix is $$ p \times p $$:

Total variance = $$ \lambda_1 + \lambda_2 + \ldots + \lambda_p $$

The $$ k $$th principal component explains: $$ \frac{\lambda_k}{\lambda_1 + \lambda_2 + \ldots + \lambda_p} $$

The first $$ k $$ principal components explain: $$ \frac{\lambda_1 + \lambda_2 + \ldots + \lambda_k}{\lambda_1 + \lambda_2 + \ldots + \lambda_p} $$

## Eigendecomposition

Principal Component Analysis (PCA) aims to reduce the dimensionality of high-dimensional data points by linearly projecting them onto a lower-dimensional space while preserving as much variance as possible or minimizing the reconstruction error made by this projection. This is achieved by performing eigendecomposition on the covariance matrix V of the dataset $$X$$, such that $$ V=PDP^T $$. Since the covariance matrix is symmetric, eigenvalues in matrix D are always positive. An eigenvector that preserves maximum variance corresponds to the largest eigenvalue.

## Singular Value Decomposition

Singular Value Decomposition (SVD) is more stable than eigendecomposition, especially when the dataset has fewer data points than dimensions. Directly performing PCA can be inefficient, so singular value decomposition (SVD) is preferred.


[some good lecture notes found](https://graphics.stanford.edu/courses/cs233-20-spring/ReferencedPapers/LectureNotes-PCA.pdf)

[lecture notes](https://people.tamu.edu/~sji/classes/PCA.pdf)
