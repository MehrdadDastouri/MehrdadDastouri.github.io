---
layout: post
title: "Prediction Error and the Hidden Cost of Dimensionality"
date: 2025-12-06
categories: [statistical-inference, linear-regression]
tags: [least-squares, prediction-mse, bias-variance, dimensionality]
math: true
---

I ran into this when testing a regression model on held-out data and the predictions were worse than I expected. The training error looked fine, but the test error kept climbing as I added more features. Eventually I worked through the math and found something unsettling: the prediction error grows linearly with the dimension of the parameter space, even when the model is correct.

Consider a standard linear regression setup where the response is

$$y = \mathbf{x}^T \boldsymbol{\theta}_o + \eta,$$

with $\eta$ drawn from a zero-mean distribution with variance $\sigma_\eta^2$. We fit the model using least squares on $N$ training samples, getting an estimate $\hat{\boldsymbol{\theta}}$. Now we want to predict the response at a new test point $\mathbf{x}$. The predicted value is

$$\hat{y} = \mathbf{x}^T \hat{\boldsymbol{\theta}},$$

and the prediction error is

$$e = y - \hat{y} = \mathbf{x}^T (\boldsymbol{\theta}_o - \hat{\boldsymbol{\theta}}) + \eta.$$

The mean squared error of this prediction, averaged over both the training data and the test noise, splits into two parts:

$$\mathbb{E}[(y - \hat{y})^2] = \mathbb{E}[(\mathbf{x}^T (\boldsymbol{\theta}_o - \hat{\boldsymbol{\theta}}))^2] + \sigma_\eta^2.$$

The second term is irreducible—it's the noise in the test point, and no estimator can eliminate it. The first term is the squared error from estimating $\boldsymbol{\theta}_o$ and depends on the variance of $\hat{\boldsymbol{\theta}}$.

For least squares with i.i.d. Gaussian noise, the estimator is

$$\hat{\boldsymbol{\theta}} = (X^T X)^{-1} X^T \mathbf{y},$$

where $X$ is the $N \times d$ design matrix. The covariance of $\hat{\boldsymbol{\theta}}$ is

$$\text{Cov}(\hat{\boldsymbol{\theta}}) = \sigma_\eta^2 (X^T X)^{-1}.$$

Plug this into the first term and you get

$$\mathbb{E}[(\mathbf{x}^T (\boldsymbol{\theta}_o - \hat{\boldsymbol{\theta}}))^2] = \sigma_\eta^2 \mathbf{x}^T (X^T X)^{-1} \mathbf{x}.$$

Combine both terms and the total prediction MSE becomes

$$\mathbb{E}[(y - \hat{y})^2] = \sigma_\eta^2 \left(1 + \mathbf{x}^T (X^T X)^{-1} \mathbf{x}\right).$$

What caught my attention here is the dependence on $\mathbf{x}^T (X^T X)^{-1} \mathbf{x}$. This quantity measures how far the test point $\mathbf{x}$ sits from the training distribution. If the training data spans the space uniformly and the test point is typical, the trace of $(X^T X)^{-1}$ scales roughly like $d/N$, where $d$ is the dimension. That means the prediction error grows as

$$\mathbb{E}[(y - \hat{y})^2] \approx \sigma_\eta^2 \left(1 + \frac{d}{N}\right).$$

Double the number of features and you double the prediction error, assuming $N$ stays fixed. This is the core of the bias-variance trade-off in high dimensions: each additional parameter adds estimation noise that propagates into the predictions, even when the model is perfectly specified.

In practice, this is why regularization helps so much in high-dimensional settings. Ridge regression or other shrinkage methods reduce the effective dimensionality of $(X^T X)^{-1}$, trading a small amount of bias for a large drop in the variance term. The optimal trade-off depends on the signal-to-noise ratio and the geometry of the training data, but the key insight is that prediction error doesn't just depend on how well you fit the training set—it depends on how stable your estimator is when extrapolating to new points.
