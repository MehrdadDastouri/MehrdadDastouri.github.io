---
title: "ML Estimation for Gaussian Mean and Variance"
date: "2025-12-13"
slug: "ml-estimation-for-gaussian-mean-and-variance"
description: "Deriving the maximum likelihood estimates for the mean and variance of a Gaussian distribution from independent observations."
tags: ["maximum-likelihood", "gaussian", "sample-mean", "sample-variance", "estimation-theory"]
math: true
---

This is one of the most fundamental calculations in statistics. Given independent Gaussian observations, what are the maximum likelihood estimates of the mean and variance? The standard answer is the sample mean and the sample variance, but a subtle issue regarding bias appears once the derivation is carried out carefully.

## Setup

Suppose we observe $N$ independent random variables $x_1, x_2, \ldots, x_N$, each generated according to a Gaussian distribution with unknown mean and variance:

$$
x_n \sim \mathcal{N}(\mu, \sigma^2)
$$

Our objective is to derive the maximum likelihood estimates of both unknown parameters.

## Likelihood Function

Independence allows us to write the joint probability density function as a product of individual densities,

$$
p(\mathbf{x}; \mu, \sigma^2)
= \prod_{n=1}^{N} \frac{1}{\sqrt{2\pi\sigma^2}}
\exp\!\left( -\frac{(x_n - \mu)^2}{2\sigma^2} \right).
$$

Taking logarithms simplifies the optimization problem and yields the log-likelihood

$$
\ell(\mu, \sigma^2)
= -\frac{N}{2}\log(2\pi)
- \frac{N}{2}\log(\sigma^2)
- \frac{1}{2\sigma^2}\sum_{n=1}^{N}(x_n - \mu)^2.
$$

## Maximization with Respect to the Mean

Differentiating the log-likelihood with respect to $\mu$ leads to

$$
\frac{\partial \ell}{\partial \mu}
= \frac{1}{\sigma^2}\sum_{n=1}^{N}(x_n - \mu).
$$

Setting the derivative equal to zero implies

$$
\sum_{n=1}^{N}(x_n - \mu) = 0,
$$

which immediately gives

$$
\hat{\mu}_{\text{ML}} = \frac{1}{N}\sum_{n=1}^{N} x_n.
$$

Thus, the ML estimate of the mean coincides with the sample mean.

## Maximization with Respect to the Variance

Next, we differentiate the log-likelihood with respect to $\sigma^2$:

$$
\frac{\partial \ell}{\partial \sigma^2}
= -\frac{N}{2\sigma^2}
+ \frac{1}{2(\sigma^2)^2}\sum_{n=1}^{N}(x_n - \mu)^2.
$$

Solving the first-order condition yields

$$
\sigma^2
= \frac{1}{N}\sum_{n=1}^{N}(x_n - \mu)^2.
$$

Since the likelihood is maximized jointly over both parameters, the unknown mean is replaced by its ML estimate. This results in the familiar estimator

$$
\hat{\sigma}^2_{\text{ML}}
= \frac{1}{N}\sum_{n=1}^{N}(x_n - \hat{\mu}_{\text{ML}})^2.
$$

The appearance of $N$ in the denominator, rather than $N-1$, is a direct consequence of maximum likelihood optimization.

## Nature of the Critical Point

The log-likelihood function is concave in $\mu$ and $\sigma^2$ over the domain $\sigma^2 > 0$. Therefore, the stationary point obtained from the first-order conditions corresponds to a global maximum, not a minimum or saddle point.

## Bias of the Estimators

The estimate of the mean is unbiased, since its expectation equals the true mean:

$$
\mathbb{E}[\hat{\mu}_{\text{ML}}] = \mu.
$$

In contrast, the variance estimator is biased. A straightforward calculation shows that

$$
\mathbb{E}[\hat{\sigma}^2_{\text{ML}}]
= \frac{N-1}{N}\sigma^2.
$$

This bias arises because the sample mean is itself estimated from the data, consuming one degree of freedom. Adjusting for this effect yields the unbiased estimator

$$
s^2
= \frac{1}{N-1}\sum_{n=1}^{N}(x_n - \hat{\mu}_{\text{ML}})^2,
$$

which differs from the ML solution by a simple scaling factor.

## Discussion

Maximum likelihood estimation focuses on maximizing the probability of the observed data rather than enforcing unbiasedness. As a result, the ML estimator of the variance is biased for finite samples, although the bias vanishes as $N$ grows. In fact, for small sample sizes, the ML estimator often achieves a lower mean squared error than the unbiased alternative.

## Concluding Remarks

This derivation highlights a general principle in estimation theory. Maximum likelihood provides a systematic and powerful framework for parameter estimation, but its finite-sample properties need not align with classical criteria such as unbiasedness. Its true strength lies in consistency, asymptotic efficiency, and broad applicability across statistical models.
