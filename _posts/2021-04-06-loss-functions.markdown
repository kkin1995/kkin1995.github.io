---
title: "A Comprehensive Guide to Machine Learning - Part 1a - Loss Functions"
date: 2021-04-06 08:20:00 +0530
author: "Karan Kinariwala"
usemathjax: true
excerpt_separator: <!--more-->
---

In the previous post on Linear Regression, I glossed over many of the details without much explanation. One such detail was the choice of our loss function - the mean squared error (mse) function. In this post, I shall show why do we choose that particular function and how it arises naturally from the problem of Linear Regression.

<!--more-->

In any machine learning problem, our task is to maximize a function known as the Likelihood which is a function of our parameters $$ \theta $$ when we know the distribution of the data. Mathematically, the likelihood function is identical to the probability of observing the data given the parameters $$ \theta $$.

$$
L(\theta | X) = P(X | \theta)
$$

where, $$ X $$ is a vector of events.

Now, if we assume that observation each of these events is independent of observing the other, we can write the likelihood function as,

$$
L(\theta | X) = P(x_{1} | \theta) P(x_{2} | \theta) ...
$$

$$
L(\theta | X) = \prod_{i = 1}^{n} P(x_{i} | \theta)
$$

Now, in the case of Linear Regression, we have to find the value of $$\theta$$ for which the likelihood function $$L(\theta , X)$$ is maximum.

Let's assume that our data is normally distributed where the mean corresponds to the linear regression model which we have to find.

$$
L(\mu , \sigma^{2} | X) = P(X | \mu, \sigma^{2})
$$

$$
L(\mu , \sigma^{2} | X) = \prod_{i = 1}^{n} P(x_{i} | \theta)
$$

$$
L(\mu , \sigma^{2} | X) = \prod_{i = 1}^{n} \frac{1}{\sqrt{2 \pi} \sigma} e^{\frac{- (x_{i} - \mu)^{2}}{2 \sigma^{2}}}
$$

This is a fairly reasonable assumption to make since a lot of data that we obtain in the real world will be normally distributed, such as, the distribution of weights, the distribution of heights or even the distribution of commute times.

Suppose, we obtain data that is not normally distributed, we can (nearly) always use the Central Limit Theorem before proceeding to our analysis.

Now, let's the logarithm of the function above to obtain,

$$
\log(L) = \sum_{i = 1}^{n} \log(\frac{1}{\sqrt{2 \pi} \sigma}) - \frac{(x_{i} - \mu)^{2}}{2 \sigma^{2}}
$$

Now consider the Linear Regression model $$ y = mx $$. In this model, we assume the y-intercept to be 0, however, the calculations that will follow will be the similar even if we consider a non-zero intercept.

$$
\log(L) = \sum_{i = 1}^{n} \log(\frac{1}{\sqrt{2 \pi} \sigma}) - \frac{(y_{i} - m x_{i})^{2}}{2 \sigma^{2}}
$$

As I showed earlier, our task is to maximize this Likelihood function $$ L(\mu, \sigma^{2}) $$. Maximizing $$ L(\mu, \sigma^{2}) $$ is equivalent to maximizing $$ log(L) $$.

Therefore, to maximize the above equation, we need only to maximize the second term,

$$
max (logL) = max (- \sum_{i = 1}^{n} (y_{i} - m x_{i})^{2})
$$

Now, maximizing the negative of the term on the right hand side is the same as minimizig the positive of the same term,

$$
max (logL) = min (\sum_{i = 1}^{n} (y_{i} - m x_{i})^{2})
$$

The equation on the right hand side is nothing but the squared error loss function. If we divide it by the number of examples, we will obtain the mean squared error function,

$$
\frac{1}{n} \sum_{i = 1}^{n} (y_{i} - m x_{i})^{2}
$$

Generalizing the above equation to include the intercept,

$$
\frac{1}{n} \sum_{i = 1}^{n} (y_{i} - (m x_{i} + c))^{2}
$$

Minimizing the above equation with respect to the parameters (the slope and the y-intercept) will give the optimum values of the parameters.

Similarly, if we can derive a likelihood function for any machine learning problem, we can also derive a loss function by maximizing the aforementioned likelihood function. In a future post, when I discuss about Logistic Regression, I will show how the cross-entropy function is the most natural choice for a loss function.

## References/Further Reading:

1. [Loss Functions - EXPLAINED ! by CodeEmporium](https://www.youtube.com/watch?v=QBbC3Cjsnjg)

2. [Maximum Likelihood Estimate in Machine Learning by Normalized Nerd](https://www.youtube.com/watch?v=2PfGO753UHk)

3. [Deep Learning Book by Ian Goodfellow, Yoshua Bengio, Aaron Courville - Page 129](https://www.deeplearningbook.org/contents/ml.html)