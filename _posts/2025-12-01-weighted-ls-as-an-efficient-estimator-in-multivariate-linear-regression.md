---
layout: post
title: "Weighted LS as an Efficient Estimator in Multivariate Linear Regression"
date: 2025-12-01
categories: [statistical-inference, estimation]
tags: [weighted-least-squares, linear-regression, maximum-likelihood, efficiency]
math: true
---

In the multivariate regression setup

$$y_n = \boldsymbol{\theta}^T \mathbf{x}_n + \eta_n, \quad n=1,2,\ldots,N,$$

the noise samples $\boldsymbol{\eta} = [\eta_1,\ldots,\eta_N]^T$ are drawn from a zero‑mean Gaussian random vector with covariance matrix $\Sigma_\eta$. The input matrix is denoted $X = [\mathbf{x}_1,\ldots,\mathbf{x}_N]^T$, and the observation vector is $\mathbf{y} = [y_1,\ldots,y_N]^T$.

When the noise is correlated, ordinary least squares ignores that structure entirely and treats every sample as equally reliable. The weighted least‑squares estimator accounts for the noise covariance explicitly. Its form is

$$\hat{\boldsymbol{\theta}} 
= \left(X^T \Sigma_\eta^{-1} X\right)^{-1} X^T \Sigma_\eta^{-1} \mathbf{y}.$$

This matches the maximum likelihood estimator exactly because the log‑likelihood for Gaussian noise with covariance $\Sigma_\eta$ is

$$\log p(\mathbf{y}|\boldsymbol{\theta})
\propto -\frac{1}{2}(\mathbf{y} - X\boldsymbol{\theta})^T \Sigma_\eta^{-1} (\mathbf{y} - X\boldsymbol{\theta}).$$

Maximizing this is equivalent to minimizing the weighted squared error, where the weighting is given by $\Sigma_\eta^{-1}$. The ML principle naturally uncovers the correct weighting scheme.

Since the noise is Gaussian, the model satisfies the regularity conditions. The Fisher information for the parameter vector $\boldsymbol{\theta}$ is

$$I(\boldsymbol{\theta})
= X^T \Sigma_\eta^{-1} X.$$

The Cramér–Rao bound for any unbiased estimator states that its covariance matrix must satisfy

$$\operatorname{Cov}(\hat{\boldsymbol{\theta}}) \succeq I(\boldsymbol{\theta})^{-1}.$$

For the weighted LS estimator, the covariance is

$$\operatorname{Cov}(\hat{\boldsymbol{\theta}})
= \left(X^T \Sigma_\eta^{-1} X\right)^{-1},$$

which is exactly the inverse of the Fisher information. This means the weighted LS estimator achieves the Cramér–Rao bound and is therefore efficient.

When the noise covariance is isotropic, meaning $\Sigma_\eta = \sigma^2 I$, the weighting matrix collapses to a scalar multiple of the identity. In that case, the ML estimator simplifies to the ordinary LS estimator

$$\hat{\boldsymbol{\theta}} 
= (X^T X)^{-1} X^T \mathbf{y},$$

because weighting by a constant does not change the optimization result. This is the only scenario where unweighted LS is optimal, and it happens because the noise geometry aligns perfectly with the Euclidean metric.
