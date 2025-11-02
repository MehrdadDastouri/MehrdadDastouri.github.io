---
layout: post
title: "Understanding the Beta Distribution: Working Through the Mean and Variance"
date: 2025-10-29 11:30:00 -0400
categories: statistics probability
tags: math beta-distribution
---

After writing about the connection between the Gamma and Beta distributions, I wanted to dig deeper into the Beta distribution itself. It's one of those distributions that shows up *everywhere* in practice – especially in Bayesian inference when you're modeling probabilities or proportions. Since it's defined on $[0, 1]$, it's perfect for representing things like success rates or probabilities.

Today I'm going to work through the derivations of its mean and variance. I know these formulas are readily available, but actually deriving them yourself gives you so much more intuition about how the distribution behaves.

## The Beta Distribution Setup

A random variable $X$ follows a Beta distribution, written as $X \sim \text{Beta}(\alpha, \beta)$, when its PDF is:

$$ f(x; \alpha, \beta) = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)}x^{\alpha-1}(1-x)^{\beta-1} $$

The parameters $\alpha$ and $\beta$ are both positive and control the shape. That fraction with all the Gamma functions? That's just the Beta function $B(\alpha, \beta)$ – it's the normalizing constant that makes sure the PDF integrates to 1.

Our goal: prove that $E[X] = \frac{\alpha}{\alpha+\beta}$ and $\text{Var}(X) = \frac{\alpha\beta}{(\alpha+\beta)^2(\alpha+\beta+1)}$.

---

## Finding the Mean

The expected value is defined as $E[X] = \int_{0}^{1} x \cdot f(x) \,dx$ (the domain is $[0,1]$ for Beta). Plugging in our PDF:

$$ E[X] = \int_0^1 x \cdot \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)}x^{\alpha-1}(1-x)^{\beta-1} \,dx $$

Let me pull out that constant term and combine the powers of $x$:

$$ E[X] = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} \int_0^1 x^{\alpha}(1-x)^{\beta-1} \,dx $$

Now here's the trick – that integral looks almost like another Beta function! If I write $x^{\alpha}$ as $x^{(\alpha+1)-1}$, then:

$$ \int_0^1 x^{(\alpha+1)-1}(1-x)^{\beta-1} \,dx = B(\alpha+1, \beta) $$

And we know the Beta function equals $\frac{\Gamma(\alpha+1)\Gamma(\beta)}{\Gamma(\alpha+1+\beta)}$. Substituting this back:

$$ E[X] = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} \cdot \frac{\Gamma(\alpha+1)\Gamma(\beta)}{\Gamma(\alpha+\beta+1)} $$

The key now is using the property $\Gamma(z+1) = z\Gamma(z)$:

$$ E[X] = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} \cdot \frac{\alpha\Gamma(\alpha)\Gamma(\beta)}{(\alpha+\beta)\Gamma(\alpha+\beta)} $$

Watch everything cancel – the $\Gamma(\alpha+\beta)$ terms, the $\Gamma(\alpha)$, and $\Gamma(\beta)$ all disappear:

$$ \boxed{E[X] = \frac{\alpha}{\alpha+\beta}} $$

Nice and clean! The mean is just $\alpha$ divided by the sum of both parameters.

---

## Tackling the Variance

For variance, I'll use $\text{Var}(X) = E[X^2] - (E[X])^2$. We have the mean already, so let's find the second moment:

$$ E[X^2] = \int_0^1 x^2 \cdot \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)}x^{\alpha-1}(1-x)^{\beta-1} \,dx $$

Same strategy – pull out the constant and combine the $x$ terms ($x^2 \cdot x^{\alpha-1} = x^{\alpha+1}$):

$$ E[X^2] = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} \int_0^1 x^{\alpha+1}(1-x)^{\beta-1} \,dx $$

This time the integral is $B(\alpha+2, \beta) = \frac{\Gamma(\alpha+2)\Gamma(\beta)}{\Gamma(\alpha+\beta+2)}$:

$$ E[X^2] = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} \cdot \frac{\Gamma(\alpha+2)\Gamma(\beta)}{\Gamma(\alpha+\beta+2)} $$

Now I need to expand those Gamma functions using the recursion property:
- $\Gamma(\alpha+2) = (\alpha+1)\alpha\Gamma(\alpha)$
- $\Gamma(\alpha+\beta+2) = (\alpha+\beta+1)(\alpha+\beta)\Gamma(\alpha+\beta)$

Substituting:

$$ E[X^2] = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} \cdot \frac{(\alpha+1)\alpha\Gamma(\alpha)\Gamma(\beta)}{(\alpha+\beta+1)(\alpha+\beta)\Gamma(\alpha+\beta)} $$

After the cancellations:

$$ E[X^2] = \frac{\alpha(\alpha+1)}{(\alpha+\beta)(\alpha+\beta+1)} $$

Now for the variance itself:

$$ \text{Var}(X) = \frac{\alpha(\alpha+1)}{(\alpha+\beta)(\alpha+\beta+1)} - \left(\frac{\alpha}{\alpha+\beta}\right)^2 $$

Getting a common denominator of $(\alpha+\beta)^2(\alpha+\beta+1)$:

$$ \text{Var}(X) = \frac{\alpha(\alpha+1)(\alpha+\beta) - \alpha^2(\alpha+\beta+1)}{(\alpha+\beta)^2(\alpha+\beta+1)} $$

Let me expand that numerator carefully:

$$ (\alpha^2+\alpha)(\alpha+\beta) - (\alpha^3+\alpha^2\beta+\alpha^2) $$
$$ = \alpha^3 + \alpha^2\beta + \alpha^2 + \alpha\beta - \alpha^3 - \alpha^2\beta - \alpha^2 $$
$$ = \alpha\beta $$

Everything simplifies beautifully to:

$$ \boxed{\text{Var}(X) = \frac{\alpha\beta}{(\alpha+\beta)^2(\alpha+\beta+1)}} $$

---

## What This Tells Us

Working through these derivations gave me a better feel for how $\alpha$ and $\beta$ control the distribution. The mean formula $\frac{\alpha}{\alpha+\beta}$ is intuitive – it's the relative weight of $\alpha$.

The variance is more interesting. Notice that it has $\alpha\beta$ in the numerator and $(\alpha+\beta)^2(\alpha+\beta+1)$ in the denominator. When both $\alpha$ and $\beta$ are large, the variance becomes small – the distribution concentrates tightly around the mean. You can think of $\alpha+\beta$ as a "concentration" or "sample size" parameter.

This makes the Beta distribution incredibly flexible for Bayesian priors – you can encode both where you think the probability is (via the mean) and how confident you are (via the concentration).

Next up, I'll explore the multivariate version of this – the Dirichlet distribution!
