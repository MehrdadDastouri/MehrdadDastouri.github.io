---
layout: post
title: "Bayesian Linear Regression with Gaussian Prior"
date: 2025-12-17
categories: [statistics, bayesian-inference]
tags: [linear-regression, conjugate-prior, posterior-distribution, multivariate-gaussian]
math: true
---

This is the multivariate extension of the conjugate Gaussian setup we saw for estimating a scalar mean. Now we have a linear regression model $y = X\theta + \eta$ where $\theta$ is a parameter vector we want to estimate, $X$ is the design matrix, and $\eta$ is Gaussian noise with $p(\eta) = \mathcal{N}(\eta | 0, \Sigma_\eta)$. We put a Gaussian prior on the parameters, $p(\theta) = \mathcal{N}(\theta | \theta_0, \Sigma_0)$, and we want to find the posterior $p(\theta | y)$.

Since $y = X\theta + \eta$ and $\eta$ is zero-mean Gaussian with covariance $\Sigma_\eta$, the likelihood of observing $y$ given $\theta$ is

$$p(y|\theta) = \mathcal{N}(y | X\theta, \Sigma_\eta)$$

The posterior is proportional to the prior times the likelihood:

$$p(\theta|y) \propto p(\theta) p(y|\theta)$$

Both terms are exponentials of quadratic forms in $\theta$, so the product will also be the exponential of a quadratic form in $\theta$. This means the posterior is Gaussian. To find its mean and covariance we need to collect terms.

The log of the prior contributes $-\frac{1}{2}(\theta - \theta_0)^T \Sigma_0^{-1} (\theta - \theta_0)$ and the log-likelihood contributes $-\frac{1}{2}(y - X\theta)^T \Sigma_\eta^{-1} (y - X\theta)$. Expanding these and keeping only terms that involve $\theta$:

$$-\frac{1}{2}\theta^T \Sigma_0^{-1} \theta + \theta^T \Sigma_0^{-1} \theta_0 - \frac{1}{2}\theta^T X^T \Sigma_\eta^{-1} X \theta + \theta^T X^T \Sigma_\eta^{-1} y$$

The quadratic terms give us the inverse of the posterior covariance:

$$\Sigma_N^{-1} = \Sigma_0^{-1} + X^T \Sigma_\eta^{-1} X$$

So the posterior covariance is

$$\Sigma_N = \left( \Sigma_0^{-1} + X^T \Sigma_\eta^{-1} X \right)^{-1}$$

The linear terms tell us that $\Sigma_N^{-1} \theta_N = \Sigma_0^{-1} \theta_0 + X^T \Sigma_\eta^{-1} y$, which gives the posterior mean:

$$\theta_N = \Sigma_N \left( \Sigma_0^{-1} \theta_0 + X^T \Sigma_\eta^{-1} y \right)$$

The posterior is therefore $p(\theta|y) = \mathcal{N}(\theta | \theta_N, \Sigma_N)$ with these parameters.

The structure makes sense. The posterior precision $\Sigma_N^{-1}$ is the sum of the prior precision and the precision contributed by the data through $X^T \Sigma_\eta^{-1} X$. The posterior mean is a precision-weighted combination of the prior mean and a term that depends on the observations. When the prior is very uncertain ($\Sigma_0$ large, so $\Sigma_0^{-1}$ small) the posterior mean approaches $(X^T \Sigma_\eta^{-1} X)^{-1} X^T \Sigma_\eta^{-1} y$, which is exactly the weighted least squares estimate. When we have very little data or very noisy observations the prior dominates and $\theta_N$ stays close to $\theta_0$.
