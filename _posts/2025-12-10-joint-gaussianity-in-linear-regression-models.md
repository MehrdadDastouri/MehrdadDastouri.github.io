---
layout: post
title: "Joint Gaussianity in Linear Regression Models"
date: 2025-12-10
categories: [statistical-inference, regression]
tags: [gaussian, linear-regression, covariance-matrix, noise-model]
math: true
---

When you first learn linear regression, it's presented as this clean model: observations equal a linear function of inputs plus noise. But there's a subtle question lurking beneath the surface that I didn't think about until much later. If the inputs and the noise are both Gaussian, is the output also Gaussian? And if we stack the inputs and outputs together, do they form a jointly Gaussian vector? The answer is yes, and working out the joint covariance matrix reveals some nice structure.

Consider the general linear regression model

$$\mathbf{y} = \Theta\mathbf{x} + \boldsymbol{\eta},$$

where $\mathbf{x}$ is a vector of jointly Gaussian random variables with covariance matrix $\Sigma_x$, the matrix $\Theta \in \mathbb{R}^{k \times l}$ contains the regression parameters, and $\boldsymbol{\eta}$ is a noise vector that's also Gaussian with zero mean and covariance matrix $\Sigma_\eta$. Crucially, we assume $\boldsymbol{\eta}$ is independent of $\mathbf{x}$.

The claim is that $\mathbf{y}$ and $\mathbf{x}$ are jointly Gaussian, and their joint covariance matrix takes the form

$$\Sigma = \begin{bmatrix} \Theta\Sigma_x\Theta^T + \Sigma_\eta & \Theta\Sigma_x \\ \Sigma_x\Theta^T & \Sigma_x \end{bmatrix}.$$

Let me work through why this is true. First, the joint Gaussianity follows from our earlier result about linear transformations. We can write the stacked vector as

$$\begin{bmatrix} \mathbf{y} \\ \mathbf{x} \end{bmatrix} = \begin{bmatrix} \Theta & I \\ I & 0 \end{bmatrix} \begin{bmatrix} \mathbf{x} \\ \boldsymbol{\eta} \end{bmatrix}.$$

Wait, that's not quite right. Let me think about this more carefully. The vector $[\mathbf{x}^T, \boldsymbol{\eta}^T]^T$ is jointly Gaussian because $\mathbf{x}$ and $\boldsymbol{\eta}$ are independent Gaussians. The joint covariance of this combined vector is block diagonal:

$$\text{Cov}\begin{bmatrix} \mathbf{x} \\ \boldsymbol{\eta} \end{bmatrix} = \begin{bmatrix} \Sigma_x & 0 \\ 0 & \Sigma_\eta \end{bmatrix}.$$

Now, $\mathbf{y} = \Theta\mathbf{x} + \boldsymbol{\eta}$ is a linear function of this joint vector. Specifically,

$$\begin{bmatrix} \mathbf{y} \\ \mathbf{x} \end{bmatrix} = \begin{bmatrix} \Theta & I \\ I & 0 \end{bmatrix} \begin{bmatrix} \mathbf{x} \\ \boldsymbol{\eta} \end{bmatrix}.$$

Since linear transformations of jointly Gaussian vectors are jointly Gaussian, we immediately get that $(\mathbf{y}, \mathbf{x})$ is jointly Gaussian.

For the covariance matrix, let's compute each block. The covariance of $\mathbf{x}$ with itself is just $\Sigma_x$—that's given.

For the covariance of $\mathbf{y}$ with itself:

$$\text{Cov}(\mathbf{y}) = \text{Cov}(\Theta\mathbf{x} + \boldsymbol{\eta}) = \Theta\text{Cov}(\mathbf{x})\Theta^T + \text{Cov}(\boldsymbol{\eta}) = \Theta\Sigma_x\Theta^T + \Sigma_\eta.$$

The cross terms vanish because $\mathbf{x}$ and $\boldsymbol{\eta}$ are independent.

For the cross-covariance between $\mathbf{y}$ and $\mathbf{x}$:

$$\text{Cov}(\mathbf{y}, \mathbf{x}) = \text{Cov}(\Theta\mathbf{x} + \boldsymbol{\eta}, \mathbf{x}) = \Theta\text{Cov}(\mathbf{x}, \mathbf{x}) + \text{Cov}(\boldsymbol{\eta}, \mathbf{x}) = \Theta\Sigma_x + 0 = \Theta\Sigma_x.$$

Again, the independence of $\boldsymbol{\eta}$ and $\mathbf{x}$ kills the second term.

The cross-covariance $\text{Cov}(\mathbf{x}, \mathbf{y}) = \text{Cov}(\mathbf{y}, \mathbf{x})^T = \Sigma_x\Theta^T$.

Putting it all together:

$$\Sigma = \begin{bmatrix} \Theta\Sigma_x\Theta^T + \Sigma_\eta & \Theta\Sigma_x \\ \Sigma_x\Theta^T & \Sigma_x \end{bmatrix}.$$

This structure has a nice interpretation. The upper-left block shows that the variance of $\mathbf{y}$ has two sources: the transformed variance of $\mathbf{x}$ and the additive noise variance. The off-diagonal blocks $\Theta\Sigma_x$ and $\Sigma_x\Theta^T$ capture how observing $\mathbf{x}$ helps predict $\mathbf{y}$—this is exactly what gets exploited when we compute the conditional expectation $\mathbb{E}[\mathbf{y} \mid \mathbf{x}]$.

In fact, using the formula for Gaussian conditional expectation from a few posts ago, we get

$$\mathbb{E}[\mathbf{y} \mid \mathbf{x}] = \mathbb{E}[\mathbf{y}] + \Theta\Sigma_x \cdot \Sigma_x^{-1}(\mathbf{x} - \mathbb{E}[\mathbf{x}]) = \mathbb{E}[\mathbf{y}] + \Theta(\mathbf{x} - \mathbb{E}[\mathbf{x}]).$$

If both $\mathbf{x}$ and $\boldsymbol{\eta}$ have zero mean, this simplifies to $\mathbb{E}[\mathbf{y} \mid \mathbf{x}] = \Theta\mathbf{x}$. So the conditional expectation recovers exactly the linear part of the model, stripping away the noise. This is why least squares works: when everything is Gaussian, the best predictor of $\mathbf{y}$ given $\mathbf{x}$ is precisely the linear function we assumed in the model.
