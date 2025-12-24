---
layout: post
title: "Bayesian Inference for Gaussian Mean with Gaussian Prior"
date: 2025-12-16
categories: [statistics, bayesian-inference]
tags: [gaussian-distribution, conjugate-prior, posterior-distribution]
math: true
---

This is the classic conjugate prior setup for the Gaussian. We have a prior belief about the mean $\mu$ which is itself Gaussian, $\mu \sim \mathcal{N}(\mu_0, \sigma_0^2)$, and then we observe data that comes from a Gaussian with that unknown mean, $p(x|\mu) = \mathcal{N}(x|\mu, \sigma^2)$. The variance $\sigma^2$ of the observations is assumed known. The question is what happens to our belief about $\mu$ after seeing $N$ observations $\mathcal{X} := \{x_1, x_2, \ldots, x_N\}$.

By Bayes' theorem the posterior is proportional to the prior times the likelihood:

\[
p(\mu|\mathcal{X}) \propto p(\mu) \prod_{n=1}^{N} p(x_n|\mu)
\]

The prior contributes a term $\exp\left(-\frac{(\mu - \mu_0)^2}{2\sigma_0^2}\right)$ and the likelihood contributes $\exp\left(-\frac{1}{2\sigma^2}\sum_{n=1}^{N}(x_n - \mu)^2\right)$. When we multiply these together we get the exponential of a sum of quadratic terms in $\mu$. This is going to be Gaussian in $\mu$, which is the whole point of conjugacy.

To find the posterior mean and variance we can expand everything and collect terms. The exponent is

\[
-\frac{(\mu - \mu_0)^2}{2\sigma_0^2} - \frac{1}{2\sigma^2}\sum_{n=1}^{N}(x_n - \mu)^2
\]

Expanding the second term, $\sum_{n=1}^{N}(x_n - \mu)^2 = \sum_{n=1}^{N}x_n^2 - 2\mu \sum_{n=1}^{N}x_n + N\mu^2$. So the full exponent becomes

\[
-\frac{\mu^2 - 2\mu\mu_0 + \mu_0^2}{2\sigma_0^2} - \frac{\sum x_n^2 - 2\mu N\bar{x} + N\mu^2}{2\sigma^2}
\]

where $\bar{x} = \frac{1}{N}\sum_{n=1}^{N}x_n$ is the sample mean. Now we group terms by powers of $\mu$. The quadratic terms in $\mu$ give

\[
-\frac{\mu^2}{2\sigma_0^2} - \frac{N\mu^2}{2\sigma^2} = -\frac{\mu^2}{2}\left(\frac{1}{\sigma_0^2} + \frac{N}{\sigma^2}\right)
\]

and the linear terms give

\[
\frac{\mu\mu_0}{\sigma_0^2} + \frac{\mu N\bar{x}}{\sigma^2} = \mu\left(\frac{\mu_0}{\sigma_0^2} + \frac{N\bar{x}}{\sigma^2}\right)
\]

Completing the square, the posterior is Gaussian with variance

\[
\sigma_N^2 = \frac{1}{\frac{1}{\sigma_0^2} + \frac{N}{\sigma^2}} = \frac{\sigma^2\sigma_0^2}{N\sigma_0^2 + \sigma^2}
\]

and mean

\[
\mu_N = \sigma_N^2 \left(\frac{\mu_0}{\sigma_0^2} + \frac{N\bar{x}}{\sigma^2}\right) = \frac{N\sigma_0^2 \bar{x} + \sigma^2 \mu_0}{N\sigma_0^2 + \sigma^2}
\]

The posterior mean is a weighted average of the prior mean $\mu_0$ and the sample mean $\bar{x}$, with weights determined by the precisions. When $N$ is large the data dominates and $\mu_N \approx \bar{x}$. When $N$ is small or when the prior is very tight the prior mean has more influence. The posterior variance shrinks as we collect more data, which is exactly what we would hope for. More observations means more certainty about $\mu$.
