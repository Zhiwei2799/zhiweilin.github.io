---
layout: post
math: true
toc: true
---
# Probability and statistic:
Probability and statistics cover a wide range of topics. Below are some excellent resources from which I learned probability:

[Richard Weber's probability notes](https://www.statslab.cam.ac.uk/~rrw1/prob/prob-weber.pdf) A very good notes written by Richard Weber

[A First Course in Probability textbook ](https://www.seyedkalali.com/wp-content/uploads/2016/11/A-First-Course-in-Probability-8th-ed.-Sheldon-Ross.pdf) An excellent introductory probability textbook

## Sum of two random variables:
Here I just wanted to provide proof for the convolution of two independent random variables:
$$T = X + Y $$

$$
\begin{align*}
F_T(t) & = P(T \leq t) \\
& = P(X + Y \leq t) \\
& = \int_{-\infty}^{\infty} \int_{-\infty}^{t-x} f(x, y) \, dy \, dx \\
& = \int_{-\infty}^{\infty} \int_{-\infty}^{t-x} f_X(x) \cdot f_Y(y) \, dy \, dx \\
& = \int_{-\infty}^{\infty} f_X(x) \int_{-\infty}^{t-x} f_Y(y) \, dy \, dx \\
& = \int_{-\infty}^{\infty} f_X(x) F_Y(t-x) \, dx,
\end{align*}
$$

$$
\frac{d}{dt} F_T(t) = \int_{-\infty}^{\infty} f_X(x) \frac{d}{dt} F_Y(t - x) \, dx = \int_{-\infty}^{\infty} f_X(x) f_Y(t - x) \, dx,
$$

## Jacobian Transformation

The Jacobian transformation is a common method used in the field of probability and statistics for variable transformation. It involves the use of the Jacobian matrix, which is a matrix of all first-order partial derivatives of a vector-valued function.

### Jacobian Matrix

Given a vector of random variables **X** = $$(X_1, X_2, ..., X_n)$$ and a vector-valued function **Y** = $$(Y_1, Y_2, ..., Y_n)$$ = **g(X)**, the Jacobian matrix **J** of **g** with respect to **X** is defined as:

$$
J = \begin{bmatrix}
\frac{\partial Y_1}{\partial X_1} & \cdots & \frac{\partial Y_1}{\partial X_n} \\
\vdots & \ddots & \vdots \\
\frac{\partial Y_n}{\partial X_1} & \cdots & \frac{\partial Y_n}{\partial X_n}
\end{bmatrix}
$$

### Jacobian Transformation Formula

The probability density function (PDF) of **Y**, denoted as $$f_Y(\mathbf{y})$$, can be transformed from the PDF of **X**, denoted as $$f_X(\mathbf{x})$$, using the formula:

$$
f_Y(\mathbf{y}) = f_X(\mathbf{g}^{-1}(\mathbf{y})) \cdot |\det(J)|
$$

where

$$
|\det(J)| \text{ is the absolute value of the determinant of the Jacobian matrix evaluated at } \mathbf{X} = \mathbf{g}^{-1}(\mathbf{y}).
$$

### Example

Consider two random variables $$X_1, X_2$$ transformed into $$Y_1, Y_2$$ through functions $$g_1, g_2$$. The Jacobian matrix **J** and its determinant are critical in converting the PDF $$f_{X_1, X_2}(x_1, x_2)$$ to$$(f_{Y_1, Y_2}(y_1, y_2)$$, as shown below:

$$
J = \begin{bmatrix}
\frac{\partial g_1}{\partial X_1} & \frac{\partial g_1}{\partial X_2} \\
\frac{\partial g_2}{\partial X_1} & \frac{\partial g_2}{\partial X_2}
\end{bmatrix}
$$

The determinant

$$
|\det(J)|
$$

is then used in the transformation formula to find the new PDF.


A reference chart of common distributions and relations between them.
<img width="552" alt="Screenshot 2024-02-27 at 10 02 05 PM" src="https://github.com/zhiweilin27/zhiweilin27.github.io/assets/111717798/f50f1344-947e-45c4-9800-130ff160f2d1">


