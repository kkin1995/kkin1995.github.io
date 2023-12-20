---
title: "A Comprehensive Guide to Machine Learning - Part 1"
date: 2021-03-23 08:20:00 +0530
author: "Karan Kinariwala"
usemathjax: true
excerpt_separator: <!--more-->
---

{% if jekyll.environment == 'production' and site.google_analytics %}
{% include analytics.html %}
{% endif %}

Except a few resources (which are pretty hard to find), the majority of resources to learn about this vast field either do not scratch the surface too much or they go deep to the point it becomes inaccesible to most people.

In the guide, I hope to create a comprehensive guide to machine learning, hopefully, in a systematic and accesible way.

<!--more-->

However, by no means, am I an expert in this field. I have started learning Machine Learning just about 3 years ago (in 2018) myself. If you do spot a mistake in any of these posts, please let me know by creating an issue in the attached GitHub repository.

## Linear Regression

In this first post, I will discuss about Linear Regression - one of the simplest algorithms we can learn and one which most of us have probably already learned it during college/university.

Linear Regression, to put it simply, is a method which enables us to find a relationship between two variables. One of the notable examples is the strong correlation between the increased use of High Fructose Corn Syrup and incidence of obesity and diabetes.

Some of you might remember from university that you used an analytical method to find such a relationship. That analytical method is the Normal Equation. A point to note, the normal equations is an analytical method to help us obtain the best fit linear solution, however, this best fit solution is still approximation since we are solving systems of equations which do not have exact solutions.

Yes, you will be right to say that using the Normal Equation, we get exact results. However, when we have a large number of dependent variables (which we will call "features" in future), computing the Normal Equation becomes very computationally expensive and we have to turn towards a not-necessarily better, but faster iterative algorithm which we will take a look at soon.

### The Normal Equation

Let us first derive the Normal Equation using some basic assumptions. We have a system of linear equations. For our purposes, the dimensionality is general. If the system of equations are two-dimensional, each solution will be a line, if the system of equations is three-dimensional, each solution will be a plane. The intersection of these solutions will be the solution to the system of equations.

Any system of linear equations can be compactly represented as matrices and vectors. For example,

$$
y = X \theta
$$

In the above equation, the matrix $$\theta$$ contains the coefficients to the dependent variables in the system of equations. The matrix $$X$$ contains the dependent variables (features). When there is only one feature, the matrix $$X$$ becomes a vector. The vector $$y$$ contains the independent variable labels. When there is only one feature, the system of equations becomes, the all too familiar, equation of a line:

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

Now, as promised, let's look at the numerical, iterative algorithm called Gradient Descent.

### Gradient Descent

Gradient Descent is an iterative algorithm that uses the first derivative of the loss function with respect to the coefficients (in this case, it is the mean squared error function that was introduced above) to find the minimum value. Similar to the Normal Equation, it finds the point where the first derivative is zero. Now, some of you will point out that the first derivative is also zero at the maximum points and the points of inflection. We will soon take a look as to why this algorithm only finds the minumum points. However, as you might have already noted, this algorithm is still susceptible to local minima and might not always converge to the global minimum.

Since the aim is to find the optimum values of the coeffiecients, the loss function is taken to be a function of the coefficients and now I will investigate how the loss function will vary with small change in the coefficients.

I again start with the mean squared error (MSE) function,

$$
MSE = \frac{1}{m} \sum_{i = 1}^{m} (y - y_{p})^{2}
$$

Earlier, I had included the y-intercept (bias) term in the $$\theta$$ matrix and also assumed that the first feature $$x_{0}$$ is 1. Now, I will seperate it out and represent our linear equation as follows, 

$$
y_{p} = \theta x + \theta_{0}
$$

where, $$\theta_{0}$$ is the y-intercept (bias). Therefore the mean squared error function becomes,

$$
MSE = \frac{1}{m} \sum_{i = 1}^{m} (y - (\theta x_{i} + \theta_{0}))^{2}
$$

Now, I take the first derivative of the MSE with respect to the coefficients $$\theta$$ and $$\theta_{0}$$.

$$
D_{\theta} = \frac{\partial MSE}{\partial \theta} = - \frac{2}{m} \sum_{i = 1}^{m} (y - (\theta x_{i} + \theta_{0})) x_{i}
$$

$$
D_{\theta_{0}} = \frac{\partial MSE}{\partial \theta_{0}} = - \frac{2}{m} \sum_{i = 1}^{m} (y - (\theta x_{i} + \theta_{0}))
$$

The quantities $$D_{\theta}$$ and $$D_{\theta_{0}}$$ are the first derivatives or gradients with respect to the coefficients. These two quantities tell us how the loss function will change when we slighly change the value of the coefficients. Now, we know that the gradient will give us the rate of steepest ascent. If we take the negative of the gradient, we obtain the rate of steepest descent.

Therefore, we now adjust the values of the coefficients by subtracting the gradients.

$$
\theta = \theta - \alpha D_{\theta}
$$

$$
\theta_{0} = \theta_{0} - \alpha D_{\theta_{0}}
$$

The $$\alpha$$ that I multiplied with the gradient is known as the learning rate and is a parameter chosen by the researcher. It is also known as the hyperparameter. It defines the size of the step that the algorithm takes in the direction of steepest descent. The larger the value of $$\alpha$$, the larger is the step taken.

The above steps (calculation of the MSE, calculation of the gradients and the update step) are iterated over a number of times (the value of which is also chosen by the researcher) until the algorithm reaches the minimum of the MSE function. The minimum of the MSE function is determined when the gradients $$D_{\theta}$$ and $$D_{\theta_{0}}$$ approach zero.

Gradient Descent is a fairly general algorithm and can be used in many different problems. Here, I have described it's use in Linear Regression. To use Gradient Descent in other problems, we need only to choose an appropriate loss function. For example, just as we have chosen the mean squared error function for Linear Regression, we choose the cross entropy loss function for Logistic Regression which is a problem involving classification.

In the next post, I will show how the mean squared error function is the most natural choice for a loss function for the problem of Linear Regression.