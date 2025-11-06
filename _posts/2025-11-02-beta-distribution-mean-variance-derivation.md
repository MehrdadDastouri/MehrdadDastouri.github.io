---
layout: post
title: "Beta Distribution Moments"
date: 2025-11-02 11:30:00 -0400
categories: statistics probability
tags: math beta-distribution
---

I've been using the Beta distribution for years – it's all over Bayesian methods, A/B testing, click-through rate models. But I realized I'd never actually derived its mean and variance myself. I know the formulas ($E[X] = \frac{\alpha}{\alpha+\beta}$ and that gnarly variance expression), but *why* do they look like that?

So I grabbed some paper and worked through the calculus. Turns out there's some satisfying algebra here.

## The Beta Distribution

A random variable $X \sim \text{Beta}(\alpha, \beta)$ has PDF:

$$ f(x; \alpha, \beta) = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)}x^{\alpha-1}(1-x)^{\beta-1} $$

Lives on $[0, 1]$, which makes it perfect for modeling probabilities. The parameters $\alpha$ and $\beta$ control the shape, and that Gamma function ratio normalizes everything.

---

## Deriving the Mean

Start with the definition: $E[X] = \int_{0}^{1} x \cdot f(x) \,dx$.

Plug in the PDF:

$$ E[X] = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} \int_0^1 x \cdot x^{\alpha-1}(1-x)^{\beta-1} \,dx $$

Combine the $x$ terms:

$$ E[X] = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} \int_0^1 x^{\alpha}(1-x)^{\beta-1} \,dx $$

That integral is almost another Beta function. Write $x^{\alpha}$ as $x^{(\alpha+1)-1}$:

$$ \int_0^1 x^{(\alpha+1)-1}(1-x)^{\beta-1} \,dx = B(\alpha+1, \beta) = \frac{\Gamma(\alpha+1)\Gamma(\beta)}{\Gamma(\alpha+\beta+1)} $$

Substitute back:

$$ E[X] = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} \cdot \frac{\Gamma(\alpha+1)\Gamma(\beta)}{\Gamma(\alpha+\beta+1)} $$

Now use $\Gamma(z+1) = z\Gamma(z)$:

$$ E[X] = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} \cdot \frac{\alpha\Gamma(\alpha)\Gamma(\beta)}{(\alpha+\beta)\Gamma(\alpha+\beta)} $$

Everything cancels beautifully:

$$ \boxed{E[X] = \frac{\alpha}{\alpha+\beta}} $$

Makes sense – the mean is just $\alpha$ relative to the total $\alpha + \beta$.

---

## The Variance

For variance: $\text{Var}(X) = E[X^2] - (E[X])^2$. Need to find $E[X^2]$:

$$ E[X^2] = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} \int_0^1 x^2 \cdot x^{\alpha-1}(1-x)^{\beta-1} \,dx $$

$$ = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} \int_0^1 x^{\alpha+1}(1-x)^{\beta-1} \,dx $$

Same trick: $B(\alpha+2, \beta) = \frac{\Gamma(\alpha+2)\Gamma(\beta)}{\Gamma(\alpha+\beta+2)}$

$$ E[X^2] = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} \cdot \frac{\Gamma(\alpha+2)\Gamma(\beta)}{\Gamma(\alpha+\beta+2)} $$

Expand the Gamma functions:
- $\Gamma(\alpha+2) = (\alpha+1)\alpha\Gamma(\alpha)$
- $\Gamma(\alpha+\beta+2) = (\alpha+\beta+1)(\alpha+\beta)\Gamma(\alpha+\beta)$

Substitute:

$$ E[X^2] = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} \cdot \frac{(\alpha+1)\alpha\Gamma(\alpha)\Gamma(\beta)}{(\alpha+\beta+1)(\alpha+\beta)\Gamma(\alpha+\beta)} $$

Cancel:

$$ E[X^2] = \frac{\alpha(\alpha+1)}{(\alpha+\beta)(\alpha+\beta+1)} $$

Now compute variance:

$$ \text{Var}(X) = \frac{\alpha(\alpha+1)}{(\alpha+\beta)(\alpha+\beta+1)} - \left(\frac{\alpha}{\alpha+\beta}\right)^2 $$

Common denominator:

$$ \text{Var}(X) = \frac{\alpha(\alpha+1)(\alpha+\beta) - \alpha^2(\alpha+\beta+1)}{(\alpha+\beta)^2(\alpha+\beta+1)} $$

Expand the numerator:

$$ (\alpha^2+\alpha)(\alpha+\beta) - (\alpha^3+\alpha^2\beta+\alpha^2) = \alpha\beta $$

$$ \boxed{\text{Var}(X) = \frac{\alpha\beta}{(\alpha+\beta)^2(\alpha+\beta+1)}} $$

---

## What I Noticed

The variance formula is interesting. When both $\alpha$ and $\beta$ get large, $(\alpha+\beta)^2$ dominates and variance shrinks. The distribution concentrates around the mean.

You can think of $\alpha + \beta$ as a "confidence" parameter. Higher values = tighter distribution. This shows up constantly when setting Bayesian priors – if you're uncertain, use small $\alpha, \beta$ (like 1, 1 for uniform). If you have strong beliefs, crank them up.

I run into this in A/B testing all the time. Start with a weak prior (Beta(1,1)), then update with actual click data. The posterior mean is literally $\frac{\alpha + \text{clicks}}{\alpha + \beta + \text{total}}$ – same formula.


