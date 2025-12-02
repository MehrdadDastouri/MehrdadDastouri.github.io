---
layout: post
title: "Sufficient Statistics for Gaussian Samples"
date: 2025-12-02
categories: [statistical-inference, estimation]
tags: [sufficient-statistics, gaussian-distribution, sample-mean, sample-variance]
math: true
---

A sufficient statistic captures all the information the data carries about a parameter without losing anything that matters for inference. The concept emerges naturally from factorization: if the likelihood factors into a part that depends only on the data through some statistic and a part that does not depend on the parameter at all, then that statistic is sufficient.

Consider a set of i.i.d samples $\mathcal{X} = \{x_1, x_2, \ldots, x_N\}$ drawn from a Gaussian distribution with mean $\mu$ and variance $\sigma^2$. Define the sample mean and two versions of sample variance:

$$S_\mu := \frac{1}{N}\sum_{n=1}^N x_n, \quad
S_{\sigma^2} := \frac{1}{N}\sum_{n=1}^N (x_n - S_\mu)^2, \quad
\bar{S}_{\sigma^2} := \frac{1}{N}\sum_{n=1}^N (x_n - \mu)^2.$$

The likelihood for all samples is

$$p(\mathcal{X}|\mu,\sigma^2)
= \prod_{n=1}^N \frac{1}{\sqrt{2\pi\sigma^2}} \exp\!\left(-\frac{(x_n - \mu)^2}{2\sigma^2}\right).$$

Expanding the exponent gives

$$\sum_{n=1}^N (x_n - \mu)^2
= \sum_{n=1}^N x_n^2 - 2\mu \sum_{n=1}^N x_n + N\mu^2.$$

The first term does not depend on the parameter, the second is linear in $S_\mu$, and the third depends only on $\mu$ and $N$. Rearranging shows that the likelihood depends on the data exclusively through $S_\mu$ and $\sum x_n^2$, which is equivalent to depending on $S_\mu$ and $S_{\sigma^2}$.

When $\mu$ is known, the structure simplifies. The sum of squared deviations from the true mean is

$$\sum_{n=1}^N (x_n - \mu)^2 = N \bar{S}_{\sigma^2}.$$

Since the likelihood factors as

$$p(\mathcal{X}|\sigma^2)
\propto (\sigma^2)^{-N/2} \exp\!\left(-\frac{N\bar{S}_{\sigma^2}}{2\sigma^2}\right),$$

the statistic $\bar{S}_{\sigma^2}$ is sufficient for $\sigma^2$ when $\mu$ is known. No other aspect of the data is needed to make optimal inferences about the variance.

When both $\mu$ and $\sigma^2$ are unknown, the pair $(S_\mu, S_{\sigma^2})$ becomes jointly sufficient. These two statistics contain all the information about the parameters that the entire sample carries. Any estimator that ignores the raw data and works only with this pair will be as good as one that uses the full dataset, which is the essence of sufficiency.
