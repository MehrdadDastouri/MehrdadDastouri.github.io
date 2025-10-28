---
layout: post
title: "Deriving the Mean and Variance of the Beta Distribution"
date: 2025-10-29 10:00:00 -0330
categories: statistics probability
---

<p>
  The Beta distribution is a fundamental continuous probability distribution defined on the interval $[0, 1]$. It is widely used to model random variables that represent proportions, percentages, or probabilities. In Bayesian inference, it serves as the conjugate prior for the Bernoulli, binomial, and geometric distributions.
</p>
<p>
  In this post, we will walk through the step-by-step derivation of the mean (expected value) and variance of the Beta distribution.
</p>

<h3>Prerequisites: PDF and the Gamma Function</h3>
<p>
  The Probability Density Function (PDF) of the Beta distribution, parameterized by shape parameters $a > 0$ and $b > 0$, is given by:
  $$ f(x; a, b) = \frac{x^{a-1}(1-x)^{b-1}}{B(a, b)} $$
  where $B(a, b)$ is the Beta function, which can be expressed using the Gamma function ($\Gamma$):
  $$ B(a, b) = \frac{\Gamma(a)\Gamma(b)}{\Gamma(a+b)} $$
  This allows us to write the PDF as:
  $$ f(x; a, b) = \frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} x^{a-1}(1-x)^{b-1} $$
  The key property of the Gamma function that we will leverage throughout our proofs is:
  $$ \Gamma(z+1) = z\Gamma(z) $$
</p>

<hr class="my-4">

<h3>Deriving the Mean ($E[X]$)</h3>
<p>
  The expected value of $X$ is defined as:
  $$ E[X] = \int_{-\infty}^{\infty} x f(x) dx = \int_0^1 x \cdot \frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} x^{a-1}(1-x)^{b-1} dx $$
  Combining the $x$ terms inside the integral, we get:
  $$ E[X] = \frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} \int_0^1 x^{a}(1-x)^{b-1} dx $$
  The integral is in the form of a Beta function, $B(a+1, b)$. Therefore, its value is:
  $$ \int_0^1 x^{a}(1-x)^{b-1} dx = \frac{\Gamma(a+1)\Gamma(b)}{\Gamma(a+1+b)} $$
  Substituting this back into the expression for $E[X]$:
  $$ E[X] = \frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} \cdot \frac{\Gamma(a+1)\Gamma(b)}{\Gamma(a+b+1)} $$
  Now, we use the property $\Gamma(z+1) = z\Gamma(z)$ to simplify $\Gamma(a+1)$ and $\Gamma(a+b+1)$:
  $$ E[X] = \frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} \cdot \frac{a\Gamma(a)\Gamma(b)}{(a+b)\Gamma(a+b)} $$
  Canceling the common Gamma terms leaves us with the final result:
  $$ E[X] = \frac{a}{a+b} $$
</p>

<h3>Deriving the Variance ($\text{Var}(X)$)</h3>
<p>
  We use the formula $\text{Var}(X) = E[X^2] - (E[X])^2$. We first need to compute the second moment, $E[X^2]$.
  $$ E[X^2] = \int_0^1 x^2 f(x) dx = \frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} \int_0^1 x^{a+1}(1-x)^{b-1} dx $$
  The integral is equal to $B(a+2, b)$, so we have:
  $$ E[X^2] = \frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} \cdot \frac{\Gamma(a+2)\Gamma(b)}{\Gamma(a+b+2)} $$
  Using the Gamma property repeatedly, $\Gamma(a+2) = (a+1)a\Gamma(a)$ and $\Gamma(a+b+2) = (a+b+1)(a+b)\Gamma(a+b)$:
  $$ E[X^2] = \frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} \cdot \frac{(a+1)a\Gamma(a)\Gamma(b)}{(a+b+1)(a+b)\Gamma(a+b)} $$
  After canceling common terms, we get:
  $$ E[X^2] = \frac{a(a+1)}{(a+b)(a+b+1)} $$
  Now, we can compute the variance:
  $$ \text{Var}(X) = E[X^2] - (E[X])^2 = \frac{a(a+1)}{(a+b)(a+b+1)} - \left(\frac{a}{a+b}\right)^2 $$
  To simplify, we find a common denominator, which is $(a+b)^2(a+b+1)$:
  $$ \text{Var}(X) = \frac{a(a+1)(a+b) - a^2(a+b+1)}{(a+b)^2(a+b+1)} $$
  The numerator expands to $ (a^3 + a^2b + a^2 + ab) - (a^3 + a^2b + a^2) = ab $. Thus, the variance is:
  $$ \text{Var}(X) = \frac{ab}{(a+b)^2(a+b+1)} $$
</p>
