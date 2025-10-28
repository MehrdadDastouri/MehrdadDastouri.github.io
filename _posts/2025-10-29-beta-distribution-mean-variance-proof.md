---
layout: post
title: "The Beta Distribution"
date: 2025-10-29 10:00:00 -0000
description: "Deriving the mean and variance of the Beta distribution using the Gamma function."
tags:
  - math
  - probability
  - statistics
---

The Beta distribution is a continuous probability distribution defined on the interval $[0, 1]$. It is parameterized by two positive shape parameters, denoted by $a$ and $b$. The probability density function (PDF) is given by:

$$ f(x; a, b) = \frac{x^{a-1}(1-x)^{b-1}}{B(a, b)} $$

where $B(a, b)$ is the Beta function, which can be expressed using the Gamma function as:

$$ B(a, b) = \frac{\Gamma(a)\Gamma(b)}{\Gamma(a+b)} $$

Here, we will derive the expected value $E[X]$ and variance $\text{Var}(X)$ for a random variable $X \sim \text{Beta}(a, b)$.

<hr>

### Expected Value (Mean)

The expected value of $X$ is calculated by integrating $x$ times the PDF over its support.

$$ E[X] = \int_0^1 x \cdot f(x; a, b) \,dx = \int_0^1 x \frac{x^{a-1}(1-x)^{b-1}}{B(a, b)} \,dx $$

We can simplify the expression inside the integral:

$$ E[X] = \frac{1}{B(a, b)} \int_0^1 x^a(1-x)^{b-1} \,dx $$

The integral part of this expression, $\int_0^1 x^a(1-x)^{b-1} \,dx$, is by definition the Beta function $B(a+1, b)$. So, we have:

$$ E[X] = \frac{B(a+1, b)}{B(a, b)} $$

Now, we expand the Beta functions using their Gamma function representation:

$$ E[X] = \frac{\frac{\Gamma(a+1)\Gamma(b)}{\Gamma(a+1+b)}}{\frac{\Gamma(a)\Gamma(b)}{\Gamma(a+b)}} = \frac{\Gamma(a+1)}{\Gamma(a)} \cdot \frac{\Gamma(a+b)}{\Gamma(a+1+b)} $$

Using the property of the Gamma function, $\Gamma(z+1) = z\Gamma(z)$, we can simplify the ratios:
*   $\Gamma(a+1) = a\Gamma(a) \implies \frac{\Gamma(a+1)}{\Gamma(a)} = a$
*   $\Gamma(a+b+1) = (a+b)\Gamma(a+b) \implies \frac{\Gamma(a+b)}{\Gamma(a+b+1)} = \frac{1}{a+b}$

Substituting these back, we get the mean:

$$ E[X] = a \cdot \frac{1}{a+b} = \frac{a}{a+b} $$

<hr>

### Variance

To find the variance, we first need to calculate the second moment, $E[X^2]$.

$$ E[X^2] = \int_0^1 x^2 \frac{x^{a-1}(1-x)^{b-1}}{B(a, b)} \,dx = \frac{1}{B(a, b)} \int_0^1 x^{a+1}(1-x)^{b-1} \,dx $$

The integral is the Beta function $B(a+2, b)$. Therefore:

$$ E[X^2] = \frac{B(a+2, b)}{B(a, b)} = \frac{\frac{\Gamma(a+2)\Gamma(b)}{\Gamma(a+2+b)}}{\frac{\Gamma(a)\Gamma(b)}{\Gamma(a+b)}} = \frac{\Gamma(a+2)}{\Gamma(a)} \cdot \frac{\Gamma(a+b)}{\Gamma(a+2+b)} $$

Using $\Gamma(a+2) = (a+1)a\Gamma(a)$ and $\Gamma(a+b+2) = (a+b+1)(a+b)\Gamma(a+b)$, we get:

$$ E[X^2] = \frac{(a+1)a\Gamma(a)}{\Gamma(a)} \cdot \frac{\Gamma(a+b)}{(a+b+1)(a+b)\Gamma(a+b)} = \frac{a(a+1)}{(a+b)(a+b+1)} $$

The variance is given by $\text{Var}(X) = E[X^2] - (E[X])^2$:

$$ \text{Var}(X) = \frac{a(a+1)}{(a+b)(a+b+1)} - \left(\frac{a}{a+b}\right)^2 $$

$$ \text{Var}(X) = \frac{a(a+1)(a+b) - a^2(a+b+1)}{(a+b)^2(a+b+1)} $$

$$ \text{Var}(X) = \frac{a[(a+1)(a+b) - a(a+b+1)]}{(a+b)^2(a+b+1)} $$

$$ \text{Var}(X) = \frac{a[ (a^2 + ab + a + b) - (a^2 + ab + a) ]}{(a+b)^2(a+b+1)} $$

$$ \text{Var}(X) = \frac{a[b]}{(a+b)^2(a+b+1)} = \frac{ab}{(a+b)^2(a+b+1)} $$

This completes the derivation for the mean and variance of the Beta distribution.
