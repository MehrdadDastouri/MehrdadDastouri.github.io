---
layout: post
title: "ML Estimation for Exponential Distribution"
date: 2025-12-15
categories: [statistics, estimation-theory]
tags: [maximum-likelihood, exponential-distribution, sufficient-statistics]
math: true
---

The exponential distribution shows up everywhere in modeling waiting times and lifetimes and anything that has the memoryless property. The density is

\[
p(x) = \begin{cases} \lambda \exp(-\lambda x), & x \geq 0 \\ 0, & x < 0 \end{cases}
\]

where $\lambda > 0$ is the rate parameter. Given $N$ independent measurements $x_1, x_2, \ldots, x_N$, we want to find the value of $\lambda$ that maximizes the likelihood.

The likelihood function is the product of the individual densities, so

\[
L(\lambda) = \prod_{n=1}^{N} \lambda \exp(-\lambda x_n) = \lambda^N \exp\left(-\lambda \sum_{n=1}^{N} x_n\right)
\]

Taking the log makes this easier to work with. The log likelihood is

\[
\ell(\lambda) = N \log \lambda - \lambda \sum_{n=1}^{N} x_n
\]

Now we differentiate with respect to $\lambda$ and set the result to zero. We get

\[
\frac{d\ell}{d\lambda} = \frac{N}{\lambda} - \sum_{n=1}^{N} x_n = 0
\]

Solving for $\lambda$ gives

\[
\hat{\lambda} = \frac{N}{\sum_{n=1}^{N} x_n} = \frac{1}{\bar{x}}
\]

So the ML estimate is just the reciprocal of the sample mean. This makes sense intuitively. The expected value of an exponential random variable is $1/\lambda$, so if the sample mean is our best guess for the expected value, then inverting it gives our best guess for $\lambda$.

One thing to notice is that the ML estimator depends on the data only through $\sum_{n=1}^{N} x_n$. This is the sufficient statistic for $\lambda$, which is what we would expect from the general theory connecting sufficiency and maximum likelihood.
