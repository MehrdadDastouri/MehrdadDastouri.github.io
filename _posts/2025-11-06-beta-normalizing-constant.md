---
layout: post
title: "The Beta Distribution's Normalizing Constant"
date: 2025-11-06
categories: [probability, distributions]
tags: [beta-distribution, normalization, gamma-function]
math: true
---

A few days ago, I worked through the mean and variance of the Beta distribution. While doing that, I kept wondering about that normalizing constant $\frac{1}{B(a,b)}$ – where does it actually come from? Why does it guarantee that the Beta pdf integrates to 1?

## The Beta Distribution

Recall that the Beta distribution has the form:

$$
\text{Beta}(x \mid a, b) = \frac{1}{B(a,b)} x^{a-1}(1-x)^{b-1}
$$

where $x \in [0,1]$ and $a, b > 0$.

The term $B(a,b)$ is called the **Beta function**, and it's defined as:

$$
B(a,b) = \int_0^1 x^{a-1}(1-x)^{b-1} \, dx
$$

## Why Do We Need It?

For any probability density function, we need:

$$
\int_0^1 \text{Beta}(x \mid a, b) \, dx = 1
$$

If we didn't have the normalizing constant, we'd have:

$$
\int_0^1 x^{a-1}(1-x)^{b-1} \, dx = B(a,b)
$$

This integral generally doesn't equal 1. So we divide by $B(a,b)$ to "normalize" it:

$$
\int_0^1 \frac{1}{B(a,b)} x^{a-1}(1-x)^{b-1} \, dx = \frac{B(a,b)}{B(a,b)} = 1
$$

Perfect! Now it's a proper probability distribution.

## Connection to the Gamma Function

The Beta function has a beautiful relationship with the Gamma function:

$$
B(a,b) = \frac{\Gamma(a)\Gamma(b)}{\Gamma(a+b)}
$$

where the Gamma function is defined as:

$$
\Gamma(z) = \int_0^\infty t^{z-1} e^{-t} \, dt
$$

For positive integers $n$, we have $\Gamma(n) = (n-1)!$.

### Why Is This Useful?

This connection is incredibly handy because:

1. **Easier computation**: Computing $\Gamma(a)\Gamma(b)/\Gamma(a+b)$ is often easier than computing the integral $B(a,b)$ directly.

2. **Special cases**: For integer values of $a$ and $b$, we can use factorials:
   
   $$
   B(a,b) = \frac{(a-1)!(b-1)!}{(a+b-1)!}
   $$

3. **Moments**: When I calculated the mean and variance earlier, I used this relationship extensively. For example:
   
   $$
   \mathbb{E}[X^k] = \frac{B(a+k, b)}{B(a,b)} = \frac{\Gamma(a+k)\Gamma(b)\Gamma(a+b)}{\Gamma(a)\Gamma(b)\Gamma(a+b+k)}
   $$

## A Quick Example

Let's verify normalization for $\text{Beta}(2, 3)$:

$$
B(2,3) = \frac{\Gamma(2)\Gamma(3)}{\Gamma(5)} = \frac{1! \cdot 2!}{4!} = \frac{2}{24} = \frac{1}{12}
$$

So the pdf is:

$$
\text{Beta}(x \mid 2, 3) = 12x(1-x)^2
$$

Let's check that it integrates to 1:

$$
\int_0^1 12x(1-x)^2 \, dx
$$

Using the substitution $u = 1-x$:

$$
= 12\int_0^1 (1-u)u^2 \, du = 12\int_0^1 (u^2 - u^3) \, du
$$

$$
= 12\left[\frac{u^3}{3} - \frac{u^4}{4}\right]_0^1 = 12\left(\frac{1}{3} - \frac{1}{4}\right) = 12 \cdot \frac{1}{12} = 1 \quad ✓
$$

It works!

## Final Thoughts

The normalizing constant might seem like just a technical detail at first, but it's actually quite elegant. The connection between the Beta and Gamma functions reveals deeper mathematical structure, and it makes calculations much more tractable.

