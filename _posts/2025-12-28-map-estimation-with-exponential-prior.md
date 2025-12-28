---
layout: post
title: "MAP Estimation with Exponential Prior"
date: 2025-12-28
categories: [statistics, bayesian-inference]
tags: [MAP-estimation, exponential-prior, gaussian-likelihood]
math: true
---

Now a non-conjugate case. We have $x_n \sim \mathcal{N}(\mu, \sigma^2)$ i.i.d. for $n = 1, \ldots, N$ but instead of a Gaussian prior on $\mu$ we use an exponential prior $p(\mu) = \lambda \exp(-\lambda \mu)$ for $\mu \geq 0$. The MAP estimate maximizes the posterior, which is proportional to the prior times the likelihood.

The log-posterior up to constants is

$$\log p(\mu | x_1, \ldots, x_N) = \log p(\mu) + \log p(x_1, \ldots, x_N | \mu)$$

The log-prior contributes $-\lambda \mu$ and the log-likelihood from the Gaussian observations is $-\frac{1}{2\sigma^2} \sum_{n=1}^{N} (x_n - \mu)^2$. So we want to maximize

$$-\lambda \mu - \frac{1}{2\sigma^2} \sum_{n=1}^{N} (x_n - \mu)^2$$

subject to $\mu \geq 0$.

Taking the derivative with respect to $\mu$ and setting it to zero:

$$-\lambda + \frac{1}{\sigma^2} \sum_{n=1}^{N} (x_n - \mu) = 0$$

$$-\lambda + \frac{N}{\sigma^2}(\bar{x} - \mu) = 0$$

where $\bar{x} = \frac{1}{N}\sum_{n=1}^{N} x_n$. Solving for $\mu$:

$$\mu = \bar{x} - \frac{\lambda \sigma^2}{N}$$

But we have the constraint $\mu \geq 0$. The objective is concave in $\mu$ (the second derivative is $-N/\sigma^2 < 0$) so if the unconstrained solution is non-negative we're done, otherwise the maximum on $\mu \geq 0$ occurs at the boundary.

The MAP estimate is

$$\hat{\mu}_{\text{MAP}} = \max\left(0, \bar{x} - \frac{\lambda \sigma^2}{N}\right)$$

The exponential prior pulls the estimate toward zero compared to the ML estimate $\bar{x}$. The shrinkage is $\lambda \sigma^2 / N$, which decreases as we get more data. When $\bar{x}$ is small enough the estimate gets clipped to zero because the prior insists $\mu$ cannot be negative.
