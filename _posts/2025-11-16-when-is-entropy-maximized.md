---
layout: post
title: "When is Entropy Maximized?"
date: 2025-11-16
categories: [information-theory, probability]
tags: [entropy, maximum-entropy, discrete-distributions]
math: true
---

The entropy of a discrete random variable $X$ taking values $x_1, \ldots, x_n$ with probabilities $p_i = P(X = x_i)$ is:

$$
H(X) = -\sum_{i=1}^{n} p_i \ln p_i
$$

A fundamental question: when is this maximized? The answer is elegant—entropy is maximized when all outcomes are equally likely.

## Setting Up the Problem

We want to maximize $H(X)$ subject to:

$$
\sum_{i=1}^{n} p_i = 1, \quad p_i > 0
$$

Using Lagrange multipliers, define:

$$
L(p_1, \ldots, p_n, \lambda) = -\sum_{i=1}^{n} p_i \ln p_i + \lambda \left(\sum_{i=1}^{n} p_i - 1\right)
$$

Take the derivative with respect to $p_j$:

$$
\frac{\partial L}{\partial p_j} = -\ln p_j - 1 + \lambda = 0
$$

So:

$$
\ln p_j = \lambda - 1 \implies p_j = e^{\lambda - 1}
$$

This is the same for all $j$, meaning all probabilities are equal. Using the constraint $\sum p_i = 1$:

$$
n \cdot e^{\lambda - 1} = 1 \implies p_j = \frac{1}{n}
$$

## The Maximum Value

When all outcomes are equiprobable, the entropy becomes:

$$
H_{\text{max}} = -\sum_{i=1}^{n} \frac{1}{n} \ln \frac{1}{n} = -n \cdot \frac{1}{n} \ln \frac{1}{n} = -\ln \frac{1}{n} = \ln n
$$

So the uniform distribution gives $H(X) = \ln n$ (or $\log_2 n$ if using bits).

## Why This Makes Sense

Entropy measures uncertainty or unpredictability. When all outcomes are equally likely, you have maximum uncertainty—no outcome is more expected than any other. Any deviation from uniformity introduces structure, which reduces entropy.

For example, if $n = 4$ and prabilities are $(0(0s
