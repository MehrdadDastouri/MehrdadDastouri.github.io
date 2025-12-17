---
title: "ML Estimation for Gaussian Mean and Variance"
date: "2025-12-13"
slug: "ml-estimation-for-gaussian-mean-and-variance"
description: "Deriving the maximum likelihood estimates for the mean and variance of a Gaussian distribution from independent observations."
tags: ["maximum-likelihood", "gaussian", "sample-mean", "sample-variance", "estimation-theory"]
math: true
---

This is one of the most fundamental calculations in statistics. Given independent Gaussian observations, what are the maximum likelihood estimates of the mean and variance? The answer is the sample mean and sample variance, but there is a subtle twist regarding bias that deserves attention.

## Setup

We observe $N$ independent random variables $x_1, x_2, \ldots, x_N$, each drawn from

$$
x_n \sim \mathcal{N}(\mu, \sigma^2)
$$

where both $\mu$ and $\sigma^2$ are unknown. Our goal is to find the ML estimates $\hat{\mu}_{\text{ML}}$ and $\hat{\sigma}^2_{\text{ML}}$.

## The Likelihood Function

Since the observations are independent, the joint pdf is the product of the marginals:

$$
p(\mathbf{x}; \mu, \sigma^2) = \prod_{n=1}^{N} \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left( -\frac{(x_n - \mu)^2}{2\sigma^2} \right)
$$

Taking the logarithm gives the log-likelihood:

$$
\ell(\mu, \sigma^2) = -\frac{N}{2}\log(2\pi) - \frac{N}{2}\log(\sigma^2) - \frac{1}{2\sigma^2}\sum_{n=1}^{N}(x_n - \mu)^2
$$

## Maximizing with Respect to $\mu$

Taking the partial derivative with respect to $\mu$:

$$
\frac{\partial \ell}{\partial \mu} = \frac{1}{\sigma^2}\sum_{n=1}^{N}(x_n - \mu)
$$

Setting this to zero:

$$
\sum_{n=1}^{N}(x_n - \mu) = 0 \implies \sum_{n=1}^{N} x_n = N\mu
$$

Therefore,

$$
\hat{\mu}_{\text{ML}} = \frac{1}{N}\sum_{n=1}^{N} x_n
$$

This is simply the sample mean.

## Maximizing with Respect to $\sigma^2$

Now take the partial derivative with respect to $\sigma^2$:

$$
\frac{\partial \ell}{\partial \sigma^2} = -\frac{N}{2\sigma^2} + \frac{1}{2(\sigma^2)^2}\sum_{n=1}^{N}(x_n - \mu)^2
$$

Setting this to zero and solving:

$$
\frac{N}{2\sigma^2} = \frac{1}{2(\sigma^2)^2}\sum_{n=1}^{N}(x_n - \mu)^2
$$

$$
N\sigma^2 = \sum_{n=1}^{N}(x_n - \mu)^2
$$

$$
\sigma^2 = \frac{1}{N}\sum_{n=1}^{N}(x_n - \mu)^2
$$

Since we are maximizing jointly, we substitute $\hat{\mu}_{\text{ML}}$ for $\mu$:

$$
\hat{\sigma}^2_{\text{ML}} = \frac{1}{N}\sum_{n=1}^{N}(x_n - \hat{\mu}_{\text{ML}})^2
$$

Notice the denominator is $N$, not $N-1$.

## Verifying the Maximum

We should confirm this is a maximum rather than a minimum or saddle point. The log-likelihood is concave in $(\mu, \sigma^2)$ over the domain $\sigma^2 > 0$. The term $-\frac{N}{2}\log(\sigma^2)$ is concave in $\sigma^2$, and the quadratic term is concave in $\mu$ for fixed $\sigma^2$. The critical point is therefore the global maximum.

## The Bias Issue

The ML estimate $\hat{\mu}_{\text{ML}}$ is unbiased:

$$
\mathbb{E}[\hat{\mu}_{\text{ML}}] = \mu
$$

However, $\hat{\sigma}^2_{\text{ML}}$ is biased:

$$
\mathbb{E}[\hat{\sigma}^2_{\text{ML}}] = \frac{N-1}{N}\sigma^2 \neq \sigma^2
$$

The bias arises because we use the estimated mean rather than the true mean in the sum of squares. This "uses up" one degree of freedom.

The unbiased estimator of variance is

$$
s^2 = \frac{1}{N-1}\sum_{n=1}^{N}(x_n - \hat{\mu}_{\text{ML}})^2 = \frac{N}{N-1}\hat{\sigma}^2_{\text{ML}}
$$

But ML does not optimize for unbiasedness. It maximizes likelihood, and these two objectives lead to different estimators here.

## Summary

For i.i.d. Gaussian observations with unknown mean and variance:

| Parameter | ML Estimate | Unbiased? |
|-----------|-------------|-----------|
| $\mu$ | $\frac{1}{N}\sum_{n=1}^{N} x_n$ | Yes |
| $\sigma^2$ | $\frac{1}{N}\sum_{n=1}^{N}(x_n - \hat{\mu})^2$ | No |

## Final Remarks

As $N \to \infty$, the bias in $\hat{\sigma}^2_{\text{ML}}$ vanishes since $\frac{N-1}{N} \to 1$. The ML estimator is asymptotically unbiased.

Interestingly, the ML estimator for $\sigma^2$ has lower MSE than the unbiased estimator $s^2$ for small $N$. Unbiasedness is not always the most important property.

This example illustrates a general theme in estimation theory. ML is a principle for finding estimators, not a guarantee of any particular finite-sample property. Its strength lies in generality and asymptotic optimality.
