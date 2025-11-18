---
layout: post
title: "Maximum Entropy for Continuous Distributions"
date: 2025-11-17
categories: [information-theory, probability]
tags: [entropy, continuous-distributions, uniform-distribution]
math: true
---

In the discrete case, we saw that entropy is maximized by the uniform distribution. What about continuous random variables? If $X$ is constrained to lie in an interval $[a, b]$, which PDF maximizes the differential entropy?

$$
h(X) = -\int_{a}^{b} p(x) \ln p(x) \, dx
$$

The answer turns out to be the uniform distribution again, but the proof has a slightly different flavor.

## Setting Up the Optimization

We want to maximize $h(X)$ subject to:

$$
\int_{a}^{b} p(x) \, dx = 1, \quad p(x) \geq 0
$$

Using calculus of variations with a Lagrange multiplier $\lambda$:

$$
L = -\int_{a}^{b} p(x) \ln p(x) \, dx + \lambda \left(\int_{a}^{b} p(x) \, dx - 1\right)
$$

Taking the functional derivative with respect to $p(x)$:

$$
\frac{\delta L}{\delta p(x)} = -\ln p(x) - 1 + \lambda = 0
$$

This gives:

$$
\ln p(x) = \lambda - 1 \implies p(x) = e^{\lambda - 1}
$$

So $p(x)$ is constant! Using the normalization constraint:

$$
\int_{a}^{b} e^{\lambda - 1} \, dx = (b-a) e^{\lambda - 1} = 1
$$

Therefore:

$$
p(x) = \frac{1}{b-a}
$$

This is exactly the uniform distribution on $[a, b]$.

## The Maximum Entropy Value

Plugging this back into the entropy formula:

$$
h_{\text{max}} = -\int_{a}^{b} \frac{1}{b-a} \ln \frac{1}{b-a} \, dx = -\frac{1}{b-a} \ln \frac{1}{b-a} \cdot (b-a) = \ln(b-a)
$$

So the maximum differential entropy is just $\ln(b-a)$—the log of the interval length.

## Why This Makes Intuitive Sense

When you have no information about where $X$ lies within $[a, b]$ beyond the constraint itself, the uniform distribution represents maximum ignorance. Any deviation from uniformity would mean you know something about where $X$ is more or less likely to be, which reduces uncertainty.

What's interesting is how this mirrors the discrete case. There, uniform over $n$ outcomes gave $\ln n$. Here, uniform over interval of length $L = b - a$ gives $\ln L$. The pattern holds: maximum entropy comes from spreading probability as evenly as possible over the allowed region.

The continuous case is trickier because we can always add more constraints (like fixing the mean or variance), and then the maximum entropy distribution changes. But with only the interval constraint, uniform wins.
