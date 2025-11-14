---
layout: post
title: "A Simple Logarithm Bound"
date: 2025-11-13
categories: [mathematics, inequalities]
tags: [logarithm, inequalities, calculus]
math: true
---

There's a basic inequality involving the natural logarithm that comes up surprisingly often:

$$
\ln x \leq x - 1
$$

for all $x > 0$. Equality holds only at $x = 1$.

## Why It's True

Define $f(x) = x - 1 - \ln x$. We want to show $f(x) \geq 0$ for all $x > 0$.

Taking the derivative:

$$
f'(x) = 1 - \frac{1}{x} = \frac{x-1}{x}
$$

So $f'(x) < 0$ when $x < 1$ and $f'(x) > 0$ when $x > 1$. This means $f$ has a global minimum at $x = 1$.

At that point:

$$
f(1) = 1 - 1 - \ln 1 = 0
$$

Since $f(x) \geq f(1) = 0$ everywhere, we get $\ln x \leq x - 1$ with equality only at $x = 1$.

## Where This Shows Up

This bound is all over information theory and statistics. For example:
- Proving Jensen's inequality for the log function (since log is concave)
- Bounding the KL divergence between distributions
- Deriving variational bounds in probabilistic inference

What I like about this inequality is how elementary the proof is—just basic calculus—but it's the foundation for a lot of deeper results. The gap $x - 1 - \ln x$ measures how far you are from the tangent line to $\ln x$ at $x=1$, and that geometric interpretation makes it intuitive why it's always non-negative.
