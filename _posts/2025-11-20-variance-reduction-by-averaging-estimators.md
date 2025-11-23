---
layout: post
title: "Variance Reduction by Averaging Estimators"
date: 2025-11-20
categories: [statistical-inference, estimation]
tags: [variance-reduction, ensemble-methods, bias-variance]
math: true
---

Here's a classic trick: if you have multiple unbiased estimators, you can *average* them to reduce variance.

## The Setup

Suppose we have $m$ unbiased estimators $\hat{\theta}_1, \ldots, \hat{\theta}_m$ of some parameter $\theta$:

$$\mathbb{E}[\hat{\theta}_i] = \theta \quad \text{for all } i$$

Assume they're **uncorrelated** and all have the same variance:

$$\text{Var}(\hat{\theta}_i) = \sigma^2 := \mathbb{E}[(\hat{\theta}_i - \theta)^T (\hat{\theta}_i - \theta)]$$

Now define the averaged estimator:

$$\bar{\theta} = \frac{1}{m} \sum_{i=1}^m \hat{\theta}_i$$

## The Claim

The variance drops by a factor of $m$.

First, check that $\bar{\theta}$ is still unbiased:

$$\mathbb{E}[\bar{\theta}] = \frac{1}{m} \sum_{i=1}^m \mathbb{E}[\hat{\theta}_i] = \frac{1}{m} \cdot m\theta = \theta$$

Now compute the variance. Since the estimators are uncorrelated:

$$\text{Var}(\bar{\theta}) = \text{Var}\left(\frac{1}{m} \sum_{i=1}^m \hat{\theta}_i\right)$$

$$= \frac{1}{m^2} \sum_{i=1}^m \text{Var}(\hat{\theta}_i) = \frac{1}{m^2} \cdot m \sigma^2$$

$$= \frac{\sigma^2}{m}$$

So the total variance of the averaged estimator is $\frac{1}{m}$ of the original variance.

## Why This Is Everywhere in ML

This is the entire idea behind bootstrap aggregating (bagging), where you train $m$ models on different subsets and average their predictions. Ensemble methods do the same thing by combining weak learners to reduce variance. Monte Carlo estimation works because you average over multiple samples to get better estimates. Even distributed learning relies on averaging gradients from multiple workers.

The punchline is that if you can get independent (or at least uncorrelated) noisy estimates, averaging them is almost always a good idea. Variance goes down, bias stays the same. That's the classic bias-variance trade-off at work, and it's one of the most reliable tricks in the ML toolkit.
