---
layout: post
title: "Linear Combinations of Independent Gaussians Stay Gaussian"
date: 2025-12-11
categories: [statistical-inference, probability-theory]
tags: [gaussian, independence, linear-combination, characteristic-function]
math: true
---

Here's a fact that feels almost too neat to be accidental: **any linear combination of independent Gaussian random variables is itself exactly Gaussian**. Not approximately Gaussian, not asymptotically Gaussian—precisely Gaussian. This closure property is one of the main reasons the normal distribution plays such a central role in probability theory and statistics.

In this post, we state this fact precisely and give a clean, self‑contained proof using characteristic functions.

Let's set up the problem. Suppose we have $n$ independent random variables $x_1, x_2, \ldots, x_n$, where each
\[
x_i \sim \mathcal{N}(\mu_i, \sigma_i^2).
\]
Now consider the linear combination
\[
y = a_1 x_1 + a_2 x_2 + \cdots + a_n x_n
  = \sum_{i=1}^{n} a_i x_i,
\]
where $a_1, \ldots, a_n$ are fixed real constants. The question is: what is the distribution of $y$?

---

## Characteristic functions

Recall that the characteristic function of a random variable $x$ is defined by
\[
\phi_x(t) = \mathbb{E}[e^{itx}].
\]
For a Gaussian random variable with mean $\mu$ and variance $\sigma^2$, the characteristic function has the closed‑form expression
\[
\phi_x(t) = \exp\!\left(i \mu t - \tfrac{1}{2}\sigma^2 t^2\right).
\]

Two simple but crucial properties of characteristic functions are all we need:

1. **Scaling.**  
   If $y = a x$, then
   \[
   \phi_y(t) = \phi_x(a t).
   \]

2. **Additivity under independence.**  
   If $x$ and $z$ are independent, then
   \[
   \phi_{x+z}(t) = \phi_x(t)\,\phi_z(t).
   \]

---

## Computing the characteristic function of the linear combination

Let us first look at each term $a_i x_i$. Since $x_i \sim \mathcal{N}(\mu_i, \sigma_i^2)$, the scaling property gives
\[
\phi_{a_i x_i}(t)
= \exp\!\left(i a_i \mu_i t - \tfrac{1}{2} a_i^2 \sigma_i^2 t^2\right).
\]

Because the variables $x_1, \ldots, x_n$ are independent, the characteristic function of their sum is the product of the individual characteristic functions:
\[
\phi_y(t)
= \prod_{i=1}^{n} \phi_{a_i x_i}(t).
\]

Multiplying the exponentials and collecting terms, we obtain
\[
\phi_y(t)
= \exp\!\left(
  i\Bigl(\sum_{i=1}^{n} a_i \mu_i\Bigr)t
  - \tfrac{1}{2}\Bigl(\sum_{i=1}^{n} a_i^2 \sigma_i^2\Bigr)t^2
\right).
\]

---

## Identifying the distribution

The expression above is exactly the characteristic function of a Gaussian random variable. Therefore,
\[
y \sim \mathcal{N}\!\left(
\sum_{i=1}^{n} a_i \mu_i,\;
\sum_{i=1}^{n} a_i^2 \sigma_i^2
\right).
\]

Since characteristic functions uniquely determine probability distributions, this confirms that the linear combination $y$ is Gaussian.

---

## Remarks and interpretation

- The formula for the mean follows from linearity of expectation and holds for any distribution.
- The variance formula, however, depends crucially on **independence**; without independence, covariance terms would appear.
- Note that we did **not** assume the vector $(x_1,\ldots,x_n)$ is jointly Gaussian. Independence together with Gaussian marginals is sufficient for this argument.
- In contrast, a stronger and different result states that any linear transformation of a *jointly Gaussian* vector is Gaussian, even without independence.

This distinction is subtle but important, and the characteristic‑function proof makes it completely transparent.

---

## Why this matters

Much of classical statistical inference rests on this closure property. Sample means, linear regression estimators, and many familiar test statistics are linear combinations of random variables. When those variables are Gaussian—or well approximated as such—the resulting quantities remain Gaussian, allowing for exact distributional analysis and clean theoretical guarantees.

This is one of the core reasons why the Gaussian distribution occupies such a privileged position in statistics.
