---
layout: post
math: true
toc: true
---

## Generalized Linear Regression:
Generalized linear regression is an extension of ordinary linear regression. Response variable can be categorical and distribution of residual can be non-normal. That's: 
- Response variable in the GLR is no longer confined to the class of normal distribution; it need only be a member of the so-called linear exponential family of distribution.
- GLR uses a link function of the response mean to be linearly related to the predcitor.
### Linear Expential Family of Distribution
Mathemtically, a distribution is said to be a member of the family of linear exponential distribution (LED) if its probability function can be displayed in the following form:
$ f(y:\theta,\phi) = exp((y\theta - b(\theta))/\phi + S(y,\phi))
where: 
y is the argument of the probability function
\theta is the paramter of interest
\phi is so-called scale parameter
b(\theta) and S(y,\phi) are function of \thate, \phi, respectively. 
\{https://en.wikipedia.org/wiki/Exponential_family} check this webiste for furthur detail. 

### Link functions
We need to connect response distribution's mean to the predcitors. this is known as link function. As its name suggests, it links the mean of the response to a linear combination of predcitors.
$$g(\mu) = Xw$$ , where g() is a link function, \mu is response mean and X are matrix of predictors w is cofficients.
the link funtion can be any monotonic function; its montonicity allows us to inverst the link function and calculate the response mean as soon as the coefficient has been estimated from the data. 
\mu = g^-1(xw) 

## logistical regression

