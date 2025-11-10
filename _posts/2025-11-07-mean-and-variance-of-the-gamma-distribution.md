---
layout: post
title: "Mean and Variance of the Gamma Distribution"
date: 2025-11-07
categories: [probability, distributions]
tags: [gamma-distribution, mean, variance, moments]
math: true
---

The Gamma distribution shows up a lot when modeling waiting times or rate parameters. The pdf is:

$$
\text{Gamma}(x \mid a, b) = \frac{b^a}{\Gamma(a)} x^{a-1} e^{-bx}, \quad a, b, x > 0
$$

Here $a$ is the shape parameter and $b$ is the rate parameter.

## Finding the Mean

To get the mean, I start with:

$$
\mathbb{E}[X] = \int_0^\infty x \cdot \frac{b^a}{\Gamma(a)} x^{a-1} e^{-bx} \, dx = \frac{b^a}{\Gamma(a)} \int_0^\infty x^a e^{-bx} \, dx
$$

The substitution $u = bx$ simplifies this. With $x = u/b$ and $dx = du/b$:

$$
= \frac{b^a}{\Gamma(a)} \int_0^\infty \left(\frac{u}{b}\right)^a e^{-u} \frac{du}{b} = \frac{1}{b \cdot \Gamma(a)} \int_0^\infty u^a e^{-u} \, du
$$

The integral gives $\Gamma(a+1) = a\Gamma(a)$, so:

$$
\mathbb{E}[X] = \frac{a\Gamma(a)}{b \cdot \Gamma(a)} = \frac{a}{b}
$$

Pretty straightforward once you do the substitution.

## Calculating the Variance

For variance, I need $\mathbb{E}[X^2]$ first:

$$
\mathbb{E}[X^2] = \frac{b^a}{\Gamma(a)} \int_0^\infty x^{a+1} e^{-bx} \, dx
$$

Same $u = bx$ trick:

$$
= \frac{1}{b^2 \cdot \Gamma(a)} \int_0^\infty u^{a+1} e^{-u} \, du = \frac{\Gamma(a+2)}{b^2 \cdot \Gamma(a)}
$$

Since $\Gamma(a+2) = (a+1)a\Gamma(a)$:

$$
\mathbb{E}[X^2] = \frac{a(a+1)}{b^2}
$$

Now variance is:

$$
\text{Var}(X) = \frac{a(a+1)}{b^2} - \left(\frac{a}{b}\right)^2 = \frac{a(a+1) - a^2}{b^2} = \frac{a}{b^2}
$$

So the mean is $a/b$ and variance is $a/b^2$. The spread depends on both parameters.

## Quick Example

For $\text{Gamma}(2, 3)$, the mean is $2/3 \approx 0.667$ and variance is $2/9 \approx 0.222$. The distribution centers around $2/3$ with moderate spread.

What's interesting is that the variance scales with $a$ but inversely with $b^2$—so higher rate parameters really tighten things up.
