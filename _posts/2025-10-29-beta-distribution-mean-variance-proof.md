---
layout: post
title: "Deriving the Mean and Variance of the Beta Distribution"
date: 2025-10-29 11:30:00 -0400
categories: statistics probability
tags: math beta-distribution
---

<p>
  Following our discussion on the relationship between the Gamma and Beta distributions, it's natural to explore the fundamental properties of the Beta distribution itself. As a continuous probability distribution defined on the interval $[0, 1]$, the Beta distribution is incredibly versatile, often used in Bayesian inference to model the probability of a success. Today, we will derive its mean (expected value) and variance.
</p>
<p>
  A random variable $X$ follows a Beta distribution, denoted as $X \sim \text{Beta}(\alpha, \beta)$, if its probability density function (PDF) is:
  $$ f(x; \alpha, \beta) = \frac{x^{\alpha-1}(1-x)^{\beta-1}}{B(\alpha, \beta)} = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)}x^{\alpha-1}(1-x)^{\beta-1} $$
  where $\alpha$ and $\beta$ are positive shape parameters, and the denominator is the Beta function, which acts as the normalizing constant. Our goal is to prove that $E[X] = \frac{\alpha}{\alpha+\beta}$ and $\text{Var}(X) = \frac{\alpha\beta}{(\alpha+\beta)^2(\alpha+\beta+1)}$.
</p>

<hr class="my-4">

<h3>Part 1: Deriving the Mean ($E[X]$)</h3>
<p>
  The expected value (mean) of a continuous random variable is defined as $E[X] = \int_{-\infty}^{\infty} x \cdot f(x) \,dx$. For the Beta distribution, the domain is $[0, 1]$, so:
  $$ E[X] = \int_0^1 x \cdot \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)}x^{\alpha-1}(1-x)^{\beta-1} \,dx $$
  We can take the constant term outside the integral and combine the $x$ terms:
  $$ E[X] = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} \int_0^1 x^{\alpha}(1-x)^{\beta-1} \,dx $$
  The integral part looks very similar to the kernel of another Beta distribution. Let's rewrite $x^{\alpha}$ as $x^{(\alpha+1)-1}$. The integral is now:
  $$ \int_0^1 x^{(\alpha+1)-1}(1-x)^{\beta-1} \,dx $$
  This integral is the definition of the Beta function $B(\alpha+1, \beta)$, which is equal to $\frac{\Gamma(\alpha+1)\Gamma(\beta)}{\Gamma(\alpha+1+\beta)}$. Substituting this back into our equation for $E[X]$:
  $$ E[X] = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} \cdot \frac{\Gamma(\alpha+1)\Gamma(\beta)}{\Gamma(\alpha+\beta+1)} $$
  To simplify, we use the key property of the Gamma function: $\Gamma(z+1) = z\Gamma(z)$. Applying this to $\Gamma(\alpha+1)$ and $\Gamma(\alpha+\beta+1)$:
  $$ E[X] = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} \cdot \frac{\alpha\Gamma(\alpha)\Gamma(\beta)}{(\alpha+\beta)\Gamma(\alpha+\beta)} $$
  Now we can cancel out the common Gamma terms ($\Gamma(\alpha+\beta)$, $\Gamma(\alpha)$, and $\Gamma(\beta)$):
  $$ E[X] = \frac{\alpha}{\alpha+\beta} $$
</p>

<h3>Part 2: Deriving the Variance ($\text{Var}(X)$)</h3>
<p>
  To find the variance, we'll use the formula $\text{Var}(X) = E[X^2] - (E[X])^2$. We already have $E[X]$, so we need to calculate the second moment, $E[X^2]$.
  $$ E[X^2] = \int_0^1 x^2 \cdot \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)}x^{\alpha-1}(1-x)^{\beta-1} \,dx $$
  Similar to the mean calculation, we pull out the constant and combine the $x$ terms ($x^2 \cdot x^{\alpha-1} = x^{\alpha+1}$):
  $$ E[X^2] = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} \int_0^1 x^{\alpha+1}(1-x)^{\beta-1} \,dx $$
  The integral is the Beta function $B(\alpha+2, \beta) = \frac{\Gamma(\alpha+2)\Gamma(\beta)}{\Gamma(\alpha+2+\beta)}$. Substituting this in:
  $$ E[X^2] = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} \cdot \frac{\Gamma(\alpha+2)\Gamma(\beta)}{\Gamma(\alpha+\beta+2)} $$
  We simplify by applying $\Gamma(z+1) = z\Gamma(z)$ multiple times:
  <ul>
    <li>$\Gamma(\alpha+2) = (\alpha+1)\Gamma(\alpha+1) = (\alpha+1)\alpha\Gamma(\alpha)$</li>
    <li>$\Gamma(\alpha+\beta+2) = (\alpha+\beta+1)\Gamma(\alpha+\beta+1) = (\alpha+\beta+1)(\alpha+\beta)\Gamma(\alpha+\beta)$</li>
  </ul>
  $$ E[X^2] = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} \cdot \frac{(\alpha+1)\alpha\Gamma(\alpha)\Gamma(\beta)}{(\alpha+\beta+1)(\alpha+\beta)\Gamma(\alpha+\beta)} $$
  After canceling terms, we get the second moment:
  $$ E[X^2] = \frac{\alpha(\alpha+1)}{(\alpha+\beta)(\alpha+\beta+1)} $$
  Finally, we can compute the variance:
  $$ \text{Var}(X) = E[X^2] - (E[X])^2 = \frac{\alpha(\alpha+1)}{(\alpha+\beta)(\alpha+\beta+1)} - \left(\frac{\alpha}{\alpha+\beta}\right)^2 $$
  To combine these fractions, we find a common denominator, which is $(\alpha+\beta)^2(\alpha+\beta+1)$:
  $$ \text{Var}(X) = \frac{\alpha(\alpha+1)(\alpha+\beta) - \alpha^2(\alpha+\beta+1)}{(\alpha+\beta)^2(\alpha+\beta+1)} $$
  Expanding the numerator:
  $$ \text{Numerator} = (\alpha^2+\alpha)(\alpha+\beta) - (\alpha^3+\alpha^2\beta+\alpha^2) $$
  $$ = (\alpha^3 + \alpha^2\beta + \alpha^2 + \alpha\beta) - \alpha^3 - \alpha^2\beta - \alpha^2 $$
  $$ = \alpha\beta $$
  Substituting the simplified numerator back, we arrive at the variance:
  $$ \text{Var}(X) = \frac{\alpha\beta}{(\alpha+\beta)^2(\alpha+\beta+1)} $$
</p>
