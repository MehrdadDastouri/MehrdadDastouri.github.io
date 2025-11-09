---
layout: post
title: "Mean and Variance of the Dirichlet Distribution"
date: 2025-11-08
categories: [probability, distributions]
tags: [dirichlet-distribution, mean, variance, moments]
math: true
---

The Dirichlet distribution is basically the multivariate version of the Beta. It's the go-to choice when you need a distribution over probability vectors—like modeling topic proportions in documents or species abundances in ecology.

The pdf for a $K$-dimensional Dirichlet is:

$$
\text{Dir}(\mathbf{x} \mid \boldsymbol{\alpha}) = \frac{\Gamma(\alpha_0)}{\prod_{k=1}^K \Gamma(\alpha_k)} \prod_{k=1}^K x_k^{\alpha_k - 1}
$$

where $\mathbf{x} = (x_1, \ldots, x_K)$ with $x_k > 0$ and $\sum_{k=1}^K x_k = 1$, and $\alpha_0 = \sum_{k=1}^K \alpha_k$.

## Finding the Mean

For the mean of $x_j$, I need:

$$
\mathbb{E}[x_j] = \int x_j \cdot \text{Dir}(\mathbf{x} \mid \boldsymbol{\alpha}) \, d\mathbf{x}
$$

Here's the trick: pulling out the normalizing constant and focusing on the part that depends on $x_j$:

$$
= \frac{\Gamma(\alpha_0)}{\prod_k \Gamma(\alpha_k)} \int x_j^{\alpha_j} \prod_{k \neq j} x_k^{\alpha_k - 1} \, d\mathbf{x}
$$

This integral looks like a Dirichlet with updated parameters $(\alpha_1, \ldots, \alpha_j + 1, \ldots, \alpha_K)$. Since the integral of any valid pdf is 1:

$$
\int x_j^{\alpha_j} \prod_{k \neq j} x_k^{\alpha_k - 1} \, d\mathbf{x} = \frac{\prod_k \Gamma(\alpha_k')}{\Gamma(\alpha_0')}
$$

where $\alpha_j' = \alpha_j + 1$ and $\alpha_0' = \alpha_0 + 1$. Simplifying:

$$
\mathbb{E}[x_j] = \frac{\Gamma(\alpha_0)}{\Gamma(\alpha_0 + 1)} \cdot \frac{\Gamma(\alpha_j + 1)}{\Gamma(\alpha_j)} = \frac{\alpha_j}{\alpha_0}
$$

So each component's mean is just its parameter divided by the sum of all parameters. Makes intuitive sense—larger $\alpha_j$ means more mass on that component.

## Computing the Variance

For variance, I need $\mathbb{E}[x_j^2]$ first:

$$
\mathbb{E}[x_j^2] = \frac{\Gamma(\alpha_0)}{\prod_k \Gamma(\alpha_k)} \int x_j^{\alpha_j + 1} \prod_{k \neq j} x_k^{\alpha_k - 1} \, d\mathbf{x}
$$

Same idea—this is a Dirichlet with $\alpha_j'' = \alpha_j + 2$ and $\alpha_0'' = \alpha_0 + 2$:

$$
\mathbb{E}[x_j^2] = \frac{\Gamma(\alpha_0)}{\Gamma(\alpha_0 + 2)} \cdot \frac{\Gamma(\alpha_j + 2)}{\Gamma(\alpha_j)} = \frac{\alpha_j(\alpha_j + 1)}{\alpha_0(\alpha_0 + 1)}
$$

Now the variance:

$$
\text{Var}(x_j) = \frac{\alpha_j(\alpha_j + 1)}{\alpha_0(\alpha_0 + 1)} - \left(\frac{\alpha_j}{\alpha_0}\right)^2
$$

Combining terms:

$$
= \frac{\alpha_j(\alpha_j + 1)\alpha_0 - \alpha_j^2(\alpha_0 + 1)}{\alpha_0^2(\alpha_0 + 1)} = \frac{\alpha_j(\alpha_0 - \alpha_j)}{\alpha_0^2(\alpha_0 + 1)}
$$

So the variance depends on both $\alpha_j$ and the total concentration $\alpha_0$. Higher $\alpha_0$ means tighter concentration around the mean.

## Quick Example

Take $\text{Dir}([2, 3, 5])$ with $\alpha_0 = 10$. The means are:

$$
\mathbb{E}[x_1] = \frac{2}{10} = 0.2, \quad \mathbb{E}[x_2] = 0.3, \quad \mathbb{E}[x_3] = 0.5
$$

For variance of $x_1$:

$$
\text{Var}(x_1) = \frac{2 \cdot 8}{100 \cdot 11} = \frac{16}{1100} \approx 0.0145
$$

The variances get smaller as $\alpha_0$ increases—so if you had $\text{Dir}([20, 30, 50])$ instead, everything would be much more concentrated around $(0.2, 0.3, 0.5)$.

What I find neat is how the variance formula shows the tradeoff: $\alpha_j$ pulls one way (larger means more variance initially), but $\alpha_0$ in the denominator pulls the other way (larger total concentration means less variance overall). It's this balance that makes the Dirichlet so flexible for modeling uncertainty in compositional data.
