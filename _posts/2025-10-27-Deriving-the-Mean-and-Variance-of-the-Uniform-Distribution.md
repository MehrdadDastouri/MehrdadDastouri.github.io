---
layout: post
title: "Deriving the Mean and Variance of the Uniform Distribution"
date: 2025-10-27 10:00:00 -0400
categories: probability statistics uniform-distribution
---

After working through the Binomial distribution yesterday, I figured it'd be worth doing the same for the Uniform distribution. It's one of those distributions that *feels* trivial – just a flat line between two points – but the actual calculations for mean and variance have some nice tricks.

The continuous uniform distribution over $[a, b]$ has PDF:

$$f(x) = \begin{cases}
\frac{1}{b-a} & \text{if } a \leq x \leq b \\
0 & \text{otherwise}
\end{cases}$$

Let me derive $E[X]$ and $\text{Var}(X)$ from scratch.

## Deriving the Mean

The expected value is straightforward integration:

$$E[X] = \int_a^b x \cdot \frac{1}{b-a} dx = \frac{1}{b-a} \int_a^b x \, dx$$

$$= \frac{1}{b-a} \left[ \frac{x^2}{2} \right]_a^b = \frac{1}{b-a} \cdot \frac{b^2 - a^2}{2}$$

Factor the numerator:

$$E[X] = \frac{1}{b-a} \cdot \frac{(b-a)(b+a)}{2} = \frac{b+a}{2}$$

$$\boxed{E[X] = \frac{a+b}{2}}$$

Makes perfect sense – the mean of a uniform distribution is just the midpoint of the interval.

## Deriving the Variance

For variance, I'll use the formula $\text{Var}(X) = E[X^2] - (E[X])^2$.

First, let me find $E[X^2]$:

$$E[X^2] = \int_a^b x^2 \cdot \frac{1}{b-a} dx = \frac{1}{b-a} \int_a^b x^2 \, dx$$

$$= \frac{1}{b-a} \left[ \frac{x^3}{3} \right]_a^b = \frac{1}{b-a} \cdot \frac{b^3 - a^3}{3}$$

Now I need to factor $b^3 - a^3$. Using the difference of cubes formula:

$$b^3 - a^3 = (b-a)(b^2 + ab + a^2)$$

So:

$$E[X^2] = \frac{1}{b-a} \cdot \frac{(b-a)(b^2 + ab + a^2)}{3} = \frac{b^2 + ab + a^2}{3}$$

Now the variance:

$$\text{Var}(X) = E[X^2] - (E[X])^2 = \frac{b^2 + ab + a^2}{3} - \left(\frac{a+b}{2}\right)^2$$

$$= \frac{b^2 + ab + a^2}{3} - \frac{a^2 + 2ab + b^2}{4}$$

To subtract these fractions, I need a common denominator (12):

$$= \frac{4(b^2 + ab + a^2) - 3(a^2 + 2ab + b^2)}{12}$$

$$= \frac{4b^2 + 4ab + 4a^2 - 3a^2 - 6ab - 3b^2}{12}$$

$$= \frac{b^2 - 2ab + a^2}{12} = \frac{(b-a)^2}{12}$$

$$\boxed{\text{Var}(X) = \frac{(b-a)^2}{12}}$$

## Why This Makes Sense

The variance depends only on the *width* of the interval $(b-a)$, not on where it's located. A uniform distribution from $[0,10]$ has the same variance as one from $[100, 110]$ – both have width 10.

The factor of $\frac{1}{12}$ is interesting. For a unit interval $[0,1]$, the variance is exactly $\frac{1}{12} \approx 0.083$. That's a useful benchmark when thinking about uncertainty in uniform random variables.

I use this all the time when initializing weights in neural networks or generating random samples for Monte Carlo simulations. Understanding where these formulas come from makes debugging sampling code much easier.


