---
layout: post
title: "The Beta Distribution's Normalizing Constant"
date: 2025-11-06
categories: [probability, distributions]
tags: [beta-distribution, normalization, gamma-function]
math: true
---

The Beta distribution has this normalizing constant $\frac{1}{B(a,b)}$ at the front. I was curious about where it comes from and why it's needed.

## The Beta Distribution

The Beta distribution is:

$$
\text{Beta}(x \mid a, b) = \frac{1}{B(a,b)} x^{a-1}(1-x)^{b-1}
$$

where $x \in [0,1]$ and $a, b > 0$.

The term $B(a,b)$ is the Beta function:

$$
B(a,b) = \int_0^1 x^{a-1}(1-x)^{b-1} \, dx
$$

## Why We Need Normalization

For any probability density, the integral over its support must equal 1. Without the normalizing constant, we'd have:

$$
\int_0^1 x^{a-1}(1-x)^{b-1} \, dx = B(a,b)
$$

This usually isn't 1, so we divide by $B(a,b)$:

$$
\int_0^1 \frac{1}{B(a,b)} x^{a-1}(1-x)^{b-1} \, dx = \frac{B(a,b)}{B(a,b)} = 1
$$

## Connection to the Gamma Function

The Beta function relates to the Gamma function:

$$
B(a,b) = \frac{\Gamma(a)\Gamma(b)}{\Gamma(a+b)}
$$

where

$$
\Gamma(z) = \int_0^\infty t^{z-1} e^{-t} \, dt
$$

For positive integers, $\Gamma(n) = (n-1)!$, so:

$$
B(a,b) = \frac{(a-1)!(b-1)!}{(a+b-1)!}
$$

This makes computation much easier. For example, when calculating moments:

$$
\mathbb{E}[X^k] = \frac{B(a+k, b)}{B(a,b)} = \frac{\Gamma(a+k)\Gamma(b)\Gamma(a+b)}{\Gamma(a)\Gamma(b)\Gamma(a+b+k)}
$$

## Example: Beta(2, 3)

For $\text{Beta}(2, 3)$:

$$
B(2,3) = \frac{\Gamma(2)\Gamma(3)}{\Gamma(5)} = \frac{1! \cdot 2!}{4!} = \frac{2}{24} = \frac{1}{12}
$$

So the pdf is:

$$
\text{Beta}(x \mid 2, 3) = 12x(1-x)^2
$$

Checking the integral:

$$
\int_0^1 12x(1-x)^2 \, dx
$$

Using $u = 1-x$:

$$
= 12\int_0^1 (1-u)u^2 \, du = 12\int_0^1 (u^2 - u^3) \, du
$$

$$
= 12\left[\frac{u^3}{3} - \frac{u^4}{4}\right]_0^1 = 12\left(\frac{1}{3} - \frac{1}{4}\right) = 1
$$

The normalizing constant does its job—the pdf integrates to 1.
