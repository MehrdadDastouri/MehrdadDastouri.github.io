---
layout: post
title: "Why the Beta Distribution Has That Weird Normalizing Constant"
date: 2025-11-06 10:30:00 -0400
categories: probability statistics
tags: beta-distribution bayesian
---

After deriving the mean and variance of the Beta distribution a few days ago, I got curious about something I'd always taken for granted: that normalizing constant.

You know how the Beta PDF is:

$$ f(x; \alpha, \beta) = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} x^{\alpha-1}(1-x)^{\beta-1} $$

That ratio of Gamma functions always felt mysterious to me. Like, why that specific form? Today I worked through the math to see where it comes from.

---

## The Beta Function

The Beta distribution gets its name from the **Beta function**, defined as:

$$ B(\alpha, \beta) = \int_0^1 x^{\alpha-1}(1-x)^{\beta-1} \, dx $$

This integral shows up constantly in probability. For the Beta distribution to be a valid PDF, we need it to integrate to 1, so we divide by $B(\alpha, \beta)$ to normalize it.

The question is: what does $B(\alpha, \beta)$ equal?

Turns out it has a beautiful connection to the Gamma function:

$$ B(\alpha, \beta) = \frac{\Gamma(\alpha)\Gamma(\beta)}{\Gamma(\alpha+\beta)} $$

Which means the normalizing constant we need is:

$$ \frac{1}{B(\alpha, \beta)} = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} $$

Let me show you why this works.

---

## Connecting Beta and Gamma Functions

Recall the **Gamma function**:

$$ \Gamma(\alpha) = \int_0^\infty t^{\alpha-1} e^{-t} \, dt $$

Here's the trick: write out $\Gamma(\alpha)$ and $\Gamma(\beta)$ as integrals and multiply them:

$$ \Gamma(\alpha)\Gamma(\beta) = \left(\int_0^\infty s^{\alpha-1} e^{-s} \, ds\right) \left(\int_0^\infty t^{\beta-1} e^{-t} \, dt\right) $$

This is a double integral:

$$ = \int_0^\infty \int_0^\infty s^{\alpha-1} t^{\beta-1} e^{-(s+t)} \, ds \, dt $$

Now comes the clever part. Make the substitution:
- $u = s + t$
- $x = \frac{s}{s+t}$

So $s = ux$ and $t = u(1-x)$. The Jacobian of this transformation is $u$.

The limits change to:
- $0 \leq x \leq 1$
- $0 \leq u < \infty$

Substitute into the integral:

$$ \Gamma(\alpha)\Gamma(\beta) = \int_0^1 \int_0^\infty (ux)^{\alpha-1} (u(1-x))^{\beta-1} e^{-u} \cdot u \, du \, dx $$

Simplify the powers:

$$ = \int_0^1 \int_0^\infty u^{\alpha-1} x^{\alpha-1} u^{\beta-1} (1-x)^{\beta-1} e^{-u} \cdot u \, du \, dx $$

$$ = \int_0^1 \int_0^\infty x^{\alpha-1}(1-x)^{\beta-1} u^{\alpha+\beta-1} e^{-u} \, du \, dx $$

Now here's the magic – this separates into two independent integrals:

$$ = \left(\int_0^1 x^{\alpha-1}(1-x)^{\beta-1} \, dx\right) \left(\int_0^\infty u^{\alpha+\beta-1} e^{-u} \, du\right) $$

Recognize these:
- First integral: $B(\alpha, \beta)$
- Second integral: $\Gamma(\alpha+\beta)$

So we get:

$$ \Gamma(\alpha)\Gamma(\beta) = B(\alpha, \beta) \cdot \Gamma(\alpha+\beta) $$

Rearrange:

$$ \boxed{B(\alpha, \beta) = \frac{\Gamma(\alpha)\Gamma(\beta)}{\Gamma(\alpha+\beta)}} $$

---

## So the Normalizing Constant Is...

Since we want $\frac{1}{B(\alpha, \beta)}$ to normalize the Beta PDF:

$$ \frac{1}{B(\alpha, \beta)} = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} $$

That's exactly the form we see in the Beta distribution! ✓

---

## Why This Matters

This result is everywhere in Bayesian statistics. The Beta distribution is the **conjugate prior** for Bernoulli and binomial likelihoods.

When you're doing A/B testing or modeling conversion rates, you're constantly updating Beta distributions. The fact that the normalizing constant has this closed form (using Gamma functions) makes all the posterior calculations tractable.

Without this relationship, we'd be stuck computing horrible integrals every time we wanted to update a prior.

---

## Quick Sanity Check

For integers, $\Gamma(n) = (n-1)!$. Let's try $\alpha = 2, \beta = 3$:

$$ B(2,3) = \frac{\Gamma(2)\Gamma(3)}{\Gamma(5)} = \frac{1! \cdot 2!}{4!} = \frac{2}{24} = \frac{1}{12} $$

We can verify this by direct integration:

$$ B(2,3) = \int_0^1 x(1-x)^2 \, dx $$

Expand $(1-x)^2 = 1 - 2x + x^2$:

$$ = \int_0^1 (x - 2x^2 + x^3) \, dx = \left[\frac{x^2}{2} - \frac{2x^3}{3} + \frac{x^4}{4}\right]_0^1 $$

$$ = \frac{1}{2} - \frac{2}{3} + \frac{1}{4} = \frac{6 - 8 + 3}{12} = \frac{1}{12} $$

Perfect match! ✓

---

That change of variables trick (from $(s,t)$ to $(u,x)$) is one of those classic probability theory moves that shows up everywhere. Same technique works for deriving the distribution of ratios, sums, and products of random variables.
