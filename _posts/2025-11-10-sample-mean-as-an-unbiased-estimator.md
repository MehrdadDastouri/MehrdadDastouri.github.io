---
layout: post
title: "Sample Mean as an Unbiased Estimator"
date: 2025-11-10
categories: [statistics, estimation]
tags: [sample-mean, unbiased-estimator, variance, convergence]
math: true
---

One of those foundational results you use all the time but don't always think about carefully: the sample mean is unbiased and its variance goes to zero as you collect more data.

Say you have $N$ i.i.d. samples $x_1, \ldots, x_N$ from some distribution with mean $\mu$ and variance $\sigma^2$. The sample mean is:

$$
\bar{x} = \frac{1}{N} \sum_{i=1}^N x_i
$$

## Why It's Unbiased

Taking expectations:

$$
\mathbb{E}[\bar{x}] = \mathbb{E}\left[\frac{1}{N} \sum_{i=1}^N x_i\right] = \frac{1}{N} \sum_{i=1}^N \mathbb{E}[x_i] = \frac{1}{N} \cdot N\mu = \mu
$$

So on average, the sample mean hits the true mean exactly. No systematic error.

## Variance of the Sample Mean

For the variance:

$$
\text{Var}(\bar{x}) = \text{Var}\left(\frac{1}{N} \sum_{i=1}^N x_i\right) = \frac{1}{N^2} \sum_{i=1}^N \text{Var}(x_i)
$$

Since the samples are independent and each has variance $\sigma^2$:

$$
= \frac{1}{N^2} \cdot N\sigma^2 = \frac{\sigma^2}{N}
$$

This is the key part: as $N \to \infty$, we get $\text{Var}(\bar{x}) \to 0$. The sample mean converges to the true mean.

## What This Means in Practice

With 100 samples, your variance is $\sigma^2/100$. With 10,000 samples, it's $\sigma^2/10000$. So you need to quadruple your data to halve your standard error—that $1/\sqrt{N}$ scaling shows up everywhere.

The nice thing is this works for *any* distribution with finite variance. Doesn't matter if it's Gaussian, exponential, or something weird. As long as $\sigma^2 < \infty$, you get convergence.

What I find elegant here is how simple the proof is, yet how powerful the result is. Just linearity of expectation and independence. But it's the backbone of basically all empirical science.
