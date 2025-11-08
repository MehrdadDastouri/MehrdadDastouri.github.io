---
layout: post
title: "Mean and Variance of the Gamma Distribution"
date: 2025-11-07
categories: [probability, distributions]
tags: [gamma-distribution, mean, variance, moments]
math: true
---

The Gamma distribution is useful for modeling positive continuous variables, especially when dealing with waiting times or rate parameters. The pdf is:

$$
\text{Gamma}(x \mid a, b) = \frac{b^a}{\Gamma(a)} x^{a-1} e^{-bx}, \quad a, b, x > 0
$$

where $a$ is the shape parameter and $b$ is the rate parameter.

## Mean of the Gamma Distribution

The mean is:

$$
\mathbb{E}[X] = \int_0^\infty x \cdot \frac{b^a}{\Gamma(a)} x^{a-1} e^{-bx} \, dx
$$

$$
= \frac{b^a}{\Gamma(a)} \int_0^\infty x^a e^{-bx} \, dx
$$

Using the substitution $u = bx$, so $x = u/b$ and $dx = du/b$:

$$
= \frac{b^a}{\Gamma(a)} \int_0^\infty \left(\frac{u}{b}\right)^a e^{-u} \frac{du}{b}
$$

$$
= \frac{b^a}{\Gamma(a)} \cdot \frac{1}{b^{a+1}} \int_0^\infty u^a e^{-u} \, du
$$

$$
= \frac{1}{b \cdot \Gamma(a)} \int_0^\infty u^a e^{-u} \, du
$$

The integral is $\Gamma(a+1) = a \Gamma(a)$, so:

$$
\mathbb{E}[X] = \frac{a \Gamma(a)}{b \cdot \Gamma(a)} = \frac{a}{b}
$$

## Variance of the Gamma Distribution

The variance is $\text{Var}(X) = \mathbb{E}[X^2] - (\mathbb{E}[X])^2$. First, we find $\mathbb{E}[X^2]$:

$$
\mathbb{E}[X^2] = \int_0^\infty x^2 \cdot \frac{b^a}{\Gamma(a)} x^{a-1} e^{-bx} \, dx
$$

$$
= \frac{b^a}{\Gamma(a)} \int_0^\infty x^{a+1} e^{-bx} \, dx
$$

Using $u = bx$ again:

$$
= \frac{b^a}{\Gamma(a)} \cdot \frac{1}{b^{a+2}} \int_0^\infty u^{a+1} e^{-u} \, du
$$

$$
= \frac{1}{b^2 \cdot \Gamma(a)} \cdot \Gamma(a+2)
$$

Since $\Gamma(a+2) = (a+1)a\Gamma(a)$:

$$
\mathbb{E}[X^2] = \frac{(a+1)a\Gamma(a)}{b^2 \cdot \Gamma(a)} = \frac{a(a+1)}{b^2}
$$

Now the variance:

$$
\text{Var}(X) = \frac{a(a+1)}{b^2} - \left(\frac{a}{b}\right)^2
$$

$$
= \frac{a(a+1)}{b^2} - \frac{a^2}{b^2} = \frac{a(a+1) - a^2}{b^2} = \frac{a}{b^2}
$$

So we have:

$$
\mathbb{E}[X] = \frac{a}{b}, \quad \sigma_X^2 = \frac{a}{b^2}
$$

## Quick Check

For $\text{Gamma}(2, 3)$:

$$
\mathbb{E}[X] = \frac{2}{3} \approx 0.667
$$

$$
\sigma_X^2 = \frac{2}{9} \approx 0.222
$$

The distribution is centered around $2/3$ with moderate spread.
