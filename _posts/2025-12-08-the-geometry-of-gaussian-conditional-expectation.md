---
layout: post
title: "The Geometry of Gaussian Conditional Expectation"
date: 2025-12-08
categories: [statistical-inference, estimation]
tags: [gaussian, conditional-expectation, covariance, linear-regression]
math: true
---

I remember the first time I saw the formula for the conditional expectation of jointly Gaussian random vectors. It looked too clean to be true—a perfectly linear function popping out of what should be a complicated integral. It took me a while to understand why this happens, and the derivation involves some satisfying matrix algebra that connects covariance structure to optimal prediction.

Suppose $\mathbf{x}$ and $\mathbf{y}$ are jointly Gaussian random vectors with mean vectors $\boldsymbol{\mu}_x$ and $\boldsymbol{\mu}_y$, and a joint covariance matrix

$$\Sigma = \mathbb{E}\left[\begin{bmatrix} \mathbf{x} - \boldsymbol{\mu}_x \\ \mathbf{y} - \boldsymbol{\mu}_y \end{bmatrix} \begin{bmatrix} (\mathbf{x} - \boldsymbol{\mu}_x)^T, (\mathbf{y} - \boldsymbol{\mu}_y)^T \end{bmatrix}\right] = \begin{bmatrix} \Sigma_x & \Sigma_{xy} \\ \Sigma_{yx} & \Sigma_y \end{bmatrix}.$$

The block $\Sigma_x$ is the covariance of $\mathbf{x}$, $\Sigma_y$ is the covariance of $\mathbf{y}$, and $\Sigma_{xy} = \Sigma_{yx}^T$ captures the cross-covariance between them.

The claim is that if $\Sigma_x$ is nonsingular and the Schur complement $\bar{\Sigma} := \Sigma_y - \Sigma_{yx} \Sigma_x^{-1} \Sigma_{xy}$ is also nonsingular, then the conditional expectation takes the form

$$\mathbb{E}[\mathbf{y} \mid \mathbf{x}] = \mathbb{E}[\mathbf{y}] + \Sigma_{yx} \Sigma_x^{-1} (\mathbf{x} - \boldsymbol{\mu}_x).$$

This is an affine function of $\mathbf{x}$. For Gaussian vectors, the optimal MSE estimator is not just some abstract nonlinear function—it's a straight line (or hyperplane) in the joint space.

The key to deriving this is the matrix inversion lemma applied to the joint precision matrix $\Sigma^{-1}$. The joint density of $(\mathbf{x}, \mathbf{y})$ is

$$p(\mathbf{x}, \mathbf{y}) \propto \exp\left(-\frac{1}{2} \begin{bmatrix} \mathbf{x} - \boldsymbol{\mu}_x \\ \mathbf{y} - \boldsymbol{\mu}_y \end{bmatrix}^T \Sigma^{-1} \begin{bmatrix} \mathbf{x} - \boldsymbol{\mu}_x \\ \mathbf{y} - \boldsymbol{\mu}_y \end{bmatrix}\right).$$

To find $p(\mathbf{y} \mid \mathbf{x})$, we need to complete the square in $\mathbf{y}$. Using the block structure of $\Sigma^{-1}$ expressed through the Schur complement, the quadratic form separates into terms involving $\mathbf{x}$ alone and terms involving $\mathbf{y}$ centered at a linear function of $\mathbf{x}$.

After working through the algebra, the conditional distribution $\mathbf{y} \mid \mathbf{x}$ turns out to be Gaussian with mean

$$\mathbb{E}[\mathbf{y} \mid \mathbf{x}] = \boldsymbol{\mu}_y + \Sigma_{yx} \Sigma_x^{-1} (\mathbf{x} - \boldsymbol{\mu}_x)$$

and covariance

$$\text{Cov}(\mathbf{y} \mid \mathbf{x}) = \Sigma_y - \Sigma_{yx} \Sigma_x^{-1} \Sigma_{xy} = \bar{\Sigma}.$$

Notice that the conditional covariance doesn't depend on $\mathbf{x}$ at all. This is a special property of Gaussians: observing $\mathbf{x}$ shifts the mean of $\mathbf{y}$ but doesn't change how spread out it is.

The scalar case makes the geometry even clearer. When $x$ and $y$ are both scalars, the formula reduces to

$$\mathbb{E}[y \mid x] = \mu_y + \frac{\alpha \sigma_y}{\sigma_x} (x - \mu_x),$$

where $\alpha$ is the correlation coefficient

$$\alpha := \frac{\mathbb{E}[(x - \mu_x)(y - \mu_y)]}{\sigma_x \sigma_y}.$$

The slope of the regression line is $\alpha \sigma_y / \sigma_x$, which tells you how many standard deviations $y$ shifts per standard deviation change in $x$, scaled by the correlation. When $\alpha = 1$, the variables are perfectly correlated and the regression line captures all the variation. When $\alpha = 0$, observing $x$ tells you nothing about $y$, so the best prediction is just the marginal mean $\mu_y$.

What I find remarkable about this result is how it explains why linear regression works so well in practice. Many real-world phenomena are approximately Gaussian, or at least their joint distributions are well-approximated by a Gaussian in the region where most of the data lives. In those settings, the optimal predictor is genuinely linear, and fitting a linear model isn't just a convenient approximation—it's exactly the right thing to do.

The formula also reveals the structure of partial correlation. The matrix $\Sigma_{yx} \Sigma_x^{-1}$ acts as a kind of projection operator that extracts from $\mathbf{x}$ exactly the information relevant for predicting $\mathbf{y}$. The residual covariance $\bar{\Sigma}$ is what's left over—the uncertainty in $\mathbf{y}$ that can't be reduced by observing $\mathbf{x}$, no matter how precisely you measure it.
