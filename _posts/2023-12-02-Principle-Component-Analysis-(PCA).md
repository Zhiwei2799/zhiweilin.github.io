---
layout: post
math: true
toc: true
---

## Principal Components Overview

Suppose we have $$ X $$ as a vector of $$p $$ random variables, then the covariance matrix $$ V$$ is $$ p \times p $$. 
We want to find a vector $$ \alpha_1 = (\alpha_11, \alpha_12, ..., \alpha_1p) $$ such that $$ \alpha_{1}^{T} X $$ gives maximum variance.

In mathematical terms, it is expressed as:

$$
\begin{align*}
\max(\text{cov}(\alpha_{1}^{T} X)) &= \max(\alpha_{1}^{T} X \alpha_{1}) \text{        such that } ||\alpha_{1}||^2 = 1 \\
&\Rightarrow L(\alpha, \lambda) = \alpha^T X \alpha - \lambda(||\alpha||^2 - 1)
\end{align*}
$$

Taking derivatives with respect to $$ \lambda $$ and $$ \alpha $$:

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
\max(\text{cov}(\alpha_{2}^{T} X)) = \max(\alpha_{2}^{T} X \alpha_2) \text{        such that } ||\alpha_2||^2 = 1 \text{ and } \alpha_{1}^{T} \alpha_2 = 0 \\
\Rightarrow L(\alpha_2, \lambda, \lambda_2) = \alpha_21}^{T} X \alpha_2 - \lambda(||\alpha_{2}||^2 - 1) - \lambda_2(\alpha_{1}^{T} \alpha_2)
$$
continues this procedure will find all $$(lambda_k, alpha_k)$$ for kth P.C. 


Given $$ X $$ is a vector of $$ P $$ and the covariance matrix is $$ p \times p $$:

Total variance = $$ \lambda_1 + \lambda_2 + \ldots + \lambda_p $$

The $$ k $$th principal component explains: $$ \frac{\lambda_k}{\lambda_1 + \lambda_2 + \ldots + \lambda_p} $$

The first $$ k $$ principal components explain: $$ \frac{\lambda_1 + \lambda_2 + \ldots + \lambda_k}{\lambda_1 + \lambda_2 + \ldots + \lambda_p} $$

## Eigendecomposition
Principal component analysis (PCA) is to reduce the dimensionality of some high-dimensional data points by linearly projecting 
them onto a lower-dimensional space while perserving maximum varinance as possible or the reconstruction error made by this projection is minimal.
This is the same having dataset X, and perform eigendecomposition on its covriance matrix. As known, covariance matrix is symmetric, 
eigenvalues are always possible. an eigenvector that perserve maximum variance is correponeded to largest eignevalue. 

## Signular Value Decompostion
Signular Value Decompostion is more stable than Eigendecomposition, especially when dataset has fewer data points than dimensions. 
doing direct PCA is very inefficient, so singular value decomposition (SVD) is perferred. 

[some good lecture notes found](https://graphics.stanford.edu/courses/cs233-20-spring/ReferencedPapers/LectureNotes-PCA.pdf)
[lecture notes](https://people.tamu.edu/~sji/classes/PCA.pdf)
