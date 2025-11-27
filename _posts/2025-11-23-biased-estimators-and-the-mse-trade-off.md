---
layout: post
title: "Biased Estimators and the MSE Trade-off"
date: 2025-11-23
categories: [statistical-inference, estimation]
tags: [bias-variance-tradeoff, mse, biased-estimators]
math: true
---

Sometimes adding bias actually helps. This exercise shows exactly when that's the case.

## The Setup

Let $\hat{\theta}_u$ be an unbiased estimator, so $\mathbb{E}[\hat{\theta}_u] = \theta_o$. Now define a biased version:

$$\hat{\theta}_b = (1 + \alpha)\hat{\theta}_u$$

The bias is straightforward:

$$\text{bias}(\hat{\theta}_b) = \mathbb{E}[\hat{\theta}_b] - \theta_o = (1 + \alpha)\theta_o - \theta_o = \alpha\theta_o$$

The MSE of the biased estimator is:

$$\text{MSE}(\hat{\theta}_b) = \text{var}(\hat{\theta}_b) + \text{bias}^2(\hat{\theta}_b)$$

Since scaling by $(1 + \alpha)$ affects variance quadratically:

$$\text{var}(\hat{\theta}_b) = (1 + \alpha)^2 \text{var}(\hat{\theta}_u) = (1 + \alpha)^2 \text{MSE}(\hat{\theta}_u)$$

where the last equality holds because $\hat{\theta}_u$ is unbiased, so its MSE equals its variance. Combining:

$$\text{MSE}(\hat{\theta}_b) = (1 + \alpha)^2 \text{MSE}(\hat{\theta}_u) + \alpha^2\theta_o^2$$

## When Does Bias Help?

We want to find when $\text{MSE}(\hat{\theta}_b) < \text{MSE}(\hat{\theta}_u)$:

$$(1 + \alpha)^2 \text{MSE}(\hat{\theta}_u) + \alpha^2\theta_o^2 < \text{MSE}(\hat{\theta}_u)$$

Expand the left side:

$$\text{MSE}(\hat{\theta}_u) + 2\alpha\text{MSE}(\hat{\theta}_u) + \alpha^2\text{MSE}(\hat{\theta}_u) + \alpha^2\theta_o^2 < \text{MSE}(\hat{\theta}_u)$$

Cancel $\text{MSE}(\hat{\theta}_u)$ from both sides:

$$2\alpha\text{MSE}(\hat{\theta}_u) + \alpha^2(\text{MSE}(\hat{\theta}_u) + \theta_o^2) < 0$$

Factor out $\alpha$:

$$\alpha\left[2\text{MSE}(\hat{\theta}_u) + \alpha(\text{MSE}(\hat{\theta}_u) + \theta_o^2)\right] < 0$$

For this product to be negative, $\alpha$ and the bracketed term must have opposite signs. If $\alpha < 0$, then:

$$2\text{MSE}(\hat{\theta}_u) + \alpha(\text{MSE}(\hat{\theta}_u) + \theta_o^2) > 0$$

Solve for $\alpha$:

$$\alpha > -\frac{2\text{MSE}(\hat{\theta}_u)}{\text{MSE}(\hat{\theta}_u) + \theta_o^2}$$

So the range where the biased estimator wins is:

$$-\frac{2\text{MSE}(\hat{\theta}_u)}{\text{MSE}(\hat{\theta}_u) + \theta_o^2} < \alpha < 0$$

This matches the given bound. The interpretation: you can shrink the unbiased estimator toward zero (negative $\alpha$) and reduce MSE, as long as you don't shrink it too much. The optimal amount of shrinkage depends on the signal-to-noise ratio $\frac{\theta_o^2}{\text{MSE}(\hat{\theta}_u)}$.
