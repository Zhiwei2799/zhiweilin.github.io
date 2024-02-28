---
layout: post
math: true
toc: true
---
# Probability and statistic:
Probability and statistics cover a wide range of topics. Below are some excellent resources from which I learned probability:
[Richard Weber's probability notes]https://www.statslab.cam.ac.uk/~rrw1/prob/prob-weber.pdf
A very good notes written by Richard Weber 
[A First Course in Probability textbook ]https://www.seyedkalali.com/wp-content/uploads/2016/11/A-First-Course-in-Probability-8th-ed.-Sheldon-Ross.pdf
An excellent introductory probability textbook

## Sum of two random variables:
Here I just wanted to provide proof for the convolution of two independent random variables:
T = X + Y
$$
F_T(t) = P(T \leq t) = P(X + Y \leq t) = \int_{-\infty}^{\infty} \int_{-\infty}^{t-x} f(x, y) \, dy \, dx = \int_{-\infty}^{\infty} \int_{-\infty}^{t-x} f_X(x) \cdot f_Y(y) \, dy \, dx = \int_{-\infty}^{\infty} f_X(x) \int_{-\infty}^{t-x} f_Y(y) \, dy \, dx = \int_{-\infty}^{\infty} f_X(x) F_Y(t-x) \, dx,
$$

$$
\frac{d}{dt} F_T(t) = \int_{-\infty}^{\infty} f_X(x) \frac{d}{dt} F_Y(t - x) \, dx = \int_{-\infty}^{\infty} f_X(x) f_Y(t - x) \, dx,
$$


