---
layout: post
title:  "A Comprehensive Guide to ML - Part 1"
date:   2021-03-23 08:20:00 +0530
categories: jekyll update
usemathjax: true
---

Except a few resources (which are pretty hard to find), the majority of resources to learn about this vast field either do not scratch the surface too much or they go deep to the point it becomes inaccesible to most people.

In the guide, I hope to create a comprehensive guide to machine learning, hopefully, in a systematic and accesible way.

However, by no means, am I an expert in this field. I have started learning Machine Learning just about 3 years ago (in 2018) myself. If you do spot a mistake in any of these posts, please let me know by creating an issue in the attached GitHub repository.

## Linear Regression

In this first post, I will discuss about Linear Regression - one of the simplest algorithms we can learn and one which most of us have probably already learned it during college/university.

Linear Regression, to put it simply, is a method which enables us to find a relationship between two variables. One of the notable examples is the strong correlation between the increased use of High Fructose Corn Syrup and incidence of obesity and diabetes.

Some of you might remember from university that you used an analytical method to find such a relationship. That analytical method is the Normal Equation. A point to note, the normal equations is an analytical method to help us obtain the best fit linear solution, however, this best fit solution is still approximation since we are solving systems of equations which do not have exact solutions.

Yes, you will be right to say that using the Normal Equation, we get exact results. However, when we have a large number of dependent variables (which we will call "features" in future), computing the Normal Equation becomes very computationally expensive and we have to turn towards a not-necessarily better, but faster iterative algorithm which we will take a look at soon.

Let us first derive the Normal Equation using some basic assumptions. We have a system of linear equations. For our purposes, the dimensionality is general. If the system of equations are two-dimensional, each solution will be a line, if the system of equations is three-dimensional, each solution will be a plane. The intersection of these solutions will be the solution to the system of equations.

Any system of linear equations can be compactly represented as matrices and vectors. For example,

$$
y = X \theta
$$

In the above equation, the matrix $$\theta$$ contains the coefficients to the dependent variables in the system of equations. The matrix $$X$$ contains the dependent variables (features). When there is only one feature, the matrix $$X$$ becomes a vector. The vector $$y$$ contains the independent variable (labels. When there is only one feature, the system of equations becomes, the all too familiar, equation of a line:

$$
y = m x
$$

where, m is the slope of the line and is analogous the $$\theta$$ in the multi-dimensional equation.

Now, returning to the problem of Linear Regression. We are given a set of dependent variables (features) and a set of independent variables (labels) and we have to find the coeffiecients to the system of equations which relates the features to the labels. In other words, we have to find the matrix $$\theta$$ as shown above.

Let's define the best fit solution as follows,

$$
y_{p} = X \theta
$$

where $$y_{p}$$ are the estimated labels according to the best fit solution.

To find the best fit line, we have to minimize the error between the line and the corresponding label. For this purpose, we use the mean squared error (mse) function,

$$
MSE = \frac{1}{m} \sum_{i = 1}^{m} (y_{p} - y)^{2}
$$

Since, the system of equations have been expressed as matrices and vectors, the above equation is nothing but the dot (inner) product and can be rewritten as follows,

$$
MSE = (y_{p} - y)^{T} (y_{p} - y)
$$

$$
MSE = (X \theta - y)^{T} (X \theta - y)
$$

Now, we use a little bit of calculus to find the minimum to the mean squared error (MSE). We take the first derivative of the MSE with respect to the coefficient matrix $$\theta$$, equate it to zero and solve for $$\theta$$.

$$
\frac{\partial MSE}{\partial \theta} = 0
$$

$$
2 X^{T} X \theta - X^{T} y - y X^{T} = 0
$$

$$
2 X^{T} X \theta - 2 X^{T} y = 0
$$

$$
X^{T} X \theta = X^{T} y
$$

$$
\theta = (X^{T} X)^{-1} X^{T} y
$$

The above equation is the Normal Equation. Earlier, I mentioned that when we have a large number of features, the method involving the normal equation becomes very computationally expensive. The reason for this is the $$(X^{T} X)^{-1}$$ term. The inversion of matrices by computers becomes more and more expensive as the size of the matrix increases. For the computer scientists, the time complexity of matrix inversion is cubic time $$ O(n^{3}) $$.