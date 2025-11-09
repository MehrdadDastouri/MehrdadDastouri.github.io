---
layout: post
title: "Mean, Variance, and Covariance of the Dirichlet Distribution"
date: 2025-11-08
categories: [probability, distributions]
tags: [dirichlet-distribution, multivariate, mean, variance, covariance]
math: true
---

The Dirichlet distribution is a multivariate generalization of the Beta distribution. It's defined over probability vectors and is widely used in Bayesian statistics, especially for modeling proportions.

## The Dirichlet Distribution

For $K$ variables $x_1, x_2, \ldots, x_K$ with $\sum_{k=1}^K x_k = 1$ and $x_k \geq 0$, the Dirichlet pdf is:

$$
\text{Dir}(\mathbf{x} \mid \boldsymbol{\alpha}) = \frac{\Gamma(\bar{a})}{{\prod_{k=1}^K \Gamma(a_k)}} \prod_{k=1}^K x_k^{a_k - 1}
$$

where $\boldsymbol{\alpha} = (a_1, a_2, \ldots, a_K)$ and $\bar{a} = \sum_{k=1}^K a_k$.

## Mean

The mean of each component $x_k$ is:

$$
\mathbb{E}[x_k] = \frac{a_k}{\bar{a}}, \quad k = 1, 2, \ldots, K
$$

### Derivation

Using the normalization property:

$$
\int \text{Dir}(\mathbf{x} \mid \boldsymbol{\alpha}) \, d\mathbf{x} = 1
$$

We can write:

$$
\mathbb{E}[x_k] = \int x_k \cdot \text{Dir}(\mathbf{x} \mid \boldsymbol{\alpha}) \, d\mathbf{x}
$$

$$
= \frac{\Gamma(\bar{a})}{\prod_{j=1}^K \Gamma(a_j)} \int x_k^{a_k} \prod_{j \neq k} x_j^{a_j - 1} \, d\mathbf{x}
$$

This integral equals:

$$
\frac{\prod_{j=1}^K \Gamma(a_j + \delta_{jk})}{\Gamma(\bar{a} + 1)}
$$

where $\delta_{jk} = 1$ if $j = k$, and $0$ otherwise. Since $\Gamma(a_k + 1) = a_k \Gamma(a_k)$ and $\Gamma(\bar{a} + 1) = \bar{a} \Gamma(\bar{a})$:

$$
\mathbb{E}[x_k] = \frac{\Gamma(\bar{a})}{\prod_{j=1}^K \Gamma(a_j)} \cdot \frac{a_k \Gamma(a_k) \prod_{j \neq k} \Gamma(a_j)}{\bar{a} \Gamma(\bar{a})}
$$

$$
= \frac{a_k}{\bar{a}}
$$

## Variance

The variance of each component is:

$$
\sigma_{x_k}^2 = \frac{a_k (\bar{a} - a_k)}{\bar{a}^2 (1 + \bar{a})}, \quad k = 1, 2, \ldots, K
$$

### Derivation

We need $\mathbb{E}[x_k^2]$:

$$
\mathbb{E}[x_k^2] = \frac{\Gamma(\bar{a})}{\prod_{j=1}^K \Gamma(a_j)} \int x_k^{a_k + 1} \prod_{j \neq k} x_j^{a_j - 1} \, d\mathbf{x}
$$

This gives:

$$
\mathbb{E}[x_k^2] = \frac{\Gamma(\bar{a})}{\prod_{j=1}^K \Gamma(a_j)} \cdot \frac{\Gamma(a_k + 2) \prod_{j \neq k} \Gamma(a_j)}{\Gamma(\bar{a} + 2)}
$$

$$
= \frac{a_k (a_k + 1)}{\bar{a} (\bar{a} + 1)}
$$

So the variance is:

$$
\sigma_{x_k}^2 = \mathbb{E}[x_k^2] - (\mathbb{E}[x_k])^2
$$

$$
= \frac{a_k (a_k + 1)}{\bar{a} (\bar{a} + 1)} - \frac{a_k^2}{\bar{a}^2}
$$

$$
= \frac{a_k (a_k + 1) \bar{a} - a_k^2 (\bar{a} + 1)}{\bar{a}^2 (\bar{a} + 1)}
$$

$$
= \frac{a_k [a_k \bar{a} + \bar{a} - a_k \bar{a} - a_k]}{\bar{a}^2 (\bar{a} + 1)}
$$

$$
= \frac{a_k (\bar{a} - a_k)}{\bar{a}^2 (1 + \bar{a})}
$$

## Covariance

For $i \neq j$, the covariance is:

$$
\text{cov}[x_i, x_j] = -\frac{a_i a_j}{\bar{a}^2 (1 + \bar{a})}
$$

### Derivation

We need $\mathbb{E}[x_i x_j]$:

$$
\mathbb{E}[x_i x_j] = \frac{\Gamma(\bar{a})}{\prod_{k=1}^K \Gamma(a_k)} \int x_i^{a_i} x_j^{a_j} \prod_{k \neq i, j} x_k^{a_k - 1} \, d\mathbf{x}
$$

$$
= \frac{\Gamma(a_i + 1) \Gamma(a_j + 1) \prod_{k \neq i,j} \Gamma(a_k)}{\Gamma(\bar{a} + 2)} \cdot \frac{\Gamma(\bar{a})}{\prod_{k=1}^K \Gamma(a_k)}
$$

$$
= \frac{a_i a_j}{\bar{a} (\bar{a} + 1)}
$$

So:

$$
\text{cov}[x_i, x_j] = \mathbb{E}[x_i x_j] - \mathbb{E}[x_i] \mathbb{E}[x_j]
$$

$$
= \frac{a_i a_j}{\bar{a} (\bar{a} + 1)} - \frac{a_i a_j}{\bar{a}^2}
$$

$$
= \frac{a_i a_j \bar{a} - a_i a_j (\bar{a} + 1)}{\bar{a}^2 (\bar{a} + 1)}
$$

$$
= -\frac{a_i a_j}{\bar{a}^2 (1 + \bar{a})}
$$

The negative covariance makes sense: since the components must sum to 1, if one increases, the others must decrease.

## Example: Dirichlet(2, 3, 5)

For $\boldsymbol{\alpha} = (2, 3, 5)$, we have $\bar{a} = 10$.

Means:

$$
\mathbb{E}[x_1] = \frac{2}{10} = 0.2, \quad \mathbb{E}[x_2] = \frac{3}{10} = 0.3, \quad \mathbb{E}[x_3] = \frac{5}{10} = 0.5
$$

Variances:

$$
\sigma_{x_1}^2 = \frac{2 \cdot 8}{100 \cdot 11} \approx 0.0145
$$

$$
\sigma_{x_2}^2 = \frac{3 \cdot 7}{100 \cdot 11} \approx 0.0191
$$

$$
\sigma_{x_3}^2 = \frac{5 \cdot 5}{100 \cdot 11} \approx 0.0227
$$

Covariances:

$$
\text{cov}[x_1, x_2] = -\frac{2 \cdot 3}{100 \cdot 11} \approx -0.0055
$$

$$
\text{cov}[x_1, x_3] = -\frac{2 \cdot 5}{100 \cdot 11} \approx -0.0091
$$

$$
\text{cov}[x_2, x_3] = -\frac{3 \cdot 5}{100 \cdot 11} \approx -0.0136
$$

The distribution is centered at $(0.2, 0.3, 0.5)$ with negative correlations between components.
