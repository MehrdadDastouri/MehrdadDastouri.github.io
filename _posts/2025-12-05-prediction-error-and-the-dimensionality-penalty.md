---
layout: post
title: "Prediction Error and the Dimensionality Penalty"
date: 2025-12-05
categories: [statistical-inference, linear-regression]
tags: [least-squares, prediction-mse, bias-variance, dimensionality]
math: true
---

I spent an afternoon debugging a regression model that looked perfect on the training set but fell apart on new data. The coefficients seemed reasonable, the residuals were small, but the predictions on held-out points had more variance than I expected. Eventually I traced it back to something subtle: the prediction error depends not just on how well you fit the model, but on the dimension of the feature space itself.

Consider a linear regression model where the response follows

$$y = \mathbf{x}^T \boldsymbol{\theta}_o + \eta,$$

with $\eta$ drawn from a zero-mean distribution with variance $\sigma_\eta^2$. Assume the noise has identity covariance, so $\Sigma_\eta = I_N$. We fit the model using the standard least squares estimator:

$$\hat{\boldsymbol{\theta}} = (X^T X)^{-1} X^T \mathbf{y},$$

where $X$ is the $N \times d$ design matrix collecting the training inputs and $\mathbf{y}$ is the vector of training responses.

Now suppose we want to predict the response at a new test point $\mathbf{x}$. The predicted value is

$$\hat{y} = \mathbf{x}^T \hat{\boldsymbol{\theta}},$$

and the prediction error is

$$e = y - \hat{y}.$$

The mean squared error of this prediction, averaged over the training data and the test noise, measures how well the estimator generalizes. Write

$$\mathbb{E}[(y - \hat{y})^2] = \mathbb{E}\left[\left(\mathbf{x}^T (\boldsymbol{\theta}_o - \hat{\boldsymbol{\theta}}) + \eta\right)^2\right].$$

Expand the square and use the fact that $\eta$ is independent of $\hat{\boldsymbol{\theta}}$ and has zero mean:

$$\mathbb{E}[(y - \hat{y})^2] = \mathbb{E}\left[(\mathbf{x}^T (\boldsymbol{\theta}_o - \hat{\boldsymbol{\theta}}))^2\right] + \sigma_\eta^2.$$

The second term is irreducible noise—no estimator can eliminate the variance in the test point itself. The first term captures the error from estimating $\boldsymbol{\theta}_o$ using the training data.

For the least squares estimator with i.i.d. Gaussian noise, the covariance is

$$\text{Cov}(\hat{\boldsymbol{\theta}}) = \sigma_\eta^2 (X^T X)^{-1}.$$

Since $\hat{\boldsymbol{\theta}}$ is unbiased, $\mathbb{E}[\hat{\boldsymbol{\theta}}] = \boldsymbol{\theta}_o$, and so

$$\mathbb{E}\left[(\mathbf{x}^T (\boldsymbol{\theta}_o - \hat{\boldsymbol{\theta}}))^2\right] = \mathbf{x}^T \text{Cov}(\hat{\boldsymbol{\theta}}) \mathbf{x} = \sigma_\eta^2 \mathbf{x}^T (X^T X)^{-1} \mathbf{x}.$$

Combine both terms and the total prediction MSE becomes

$$\mathbb{E}[(y - \hat{y})^2] = \sigma_\eta^2 \left(1 + \mathbf{x}^T (X^T X)^{-1} \mathbf{x}\right).$$

What caught my attention here is the term $\mathbf{x}^T (X^T X)^{-1} \mathbf{x}$. This measures how far the test point sits from the centroid of the training distribution. If the training data spans the feature space uniformly and the test point is typical, then $(X^T X)^{-1}$ has trace roughly proportional to $d/N$, where $d$ is the dimension. That means the prediction error grows linearly with the number of features:

$$\mathbb{E}[(y - \hat{y})^2] \approx \sigma_\eta^2 \left(1 + \frac{d}{N}\right).$$

Double the dimension and you roughly double the prediction error, assuming the sample size stays fixed. This is the dimensionality penalty in regression: each additional feature adds estimation noise that propagates into the predictions, even when the model is correctly specified.

The expectation is taken with respect to the training data and the test noise. If you condition on a specific test point $\mathbf{x}$, the MSE depends on its position relative to the training distribution. Points near the center of the training cloud have lower error, while extrapolating far from the training region inflates $\mathbf{x}^T (X^T X)^{-1} \mathbf{x}$ and drives the MSE up.

In practice, this explains why regularization helps so much when the dimension is large relative to the sample size. Ridge regression or other shrinkage methods reduce the effective dimensionality of $(X^T X)^{-1}$, trading a small amount of bias for a large drop in variance. The optimal trade-off depends on the signal-to-noise ratio and the geometry of the training data, but the key insight is that prediction error isn't just about fitting the training set—it's about how stable your estimator is when you move to new points.
