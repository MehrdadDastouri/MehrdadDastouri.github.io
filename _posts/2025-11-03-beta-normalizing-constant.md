---
layout: post
title: "Beta Distribution Normalizing Constant"
date: 2025-11-03
categories: [probability, distributions]
tags: [beta-distribution, bayesian, conjugate-priors]
math: true
---

## Problem 2.5: Beta Distribution Normalizing Constant

Today I worked on showing that the normalizing constant in the beta distribution with parameters $a$ and $b$ is:

$$\frac{\Gamma(a + b)}{\Gamma(a)\Gamma(b)}$$

This might seem like a minor detail, but it's actually pretty important when you're working with Bayesian inference—especially when you need to compute posteriors or marginal likelihoods.

---

### The Beta PDF

The beta distribution is defined as:

$$\text{Beta}(x \mid a, b) = \frac{1}{B(a,b)} x^{a-1}(1-x)^{b-1}, \quad 0 \leq x \leq 1$$

where $B(a,b)$ is the **beta function**, which serves as the normalizing constant to ensure the PDF integrates to 1.

Our goal is to show that:

$$B(a,b) = \frac{\Gamma(a)\Gamma(b)}{\Gamma(a+b)}$$

---

### Step 1: Start with the Beta Function Definition

By definition, the beta function is:

$$B(a,b) = \int_0^1 x^{a-1}(1-x)^{b-1} \, dx$$

This integral ensures that the beta PDF is properly normalized.

---

### Step 2: Connect to the Gamma Function

Recall the **gamma function**:

$$\Gamma(a) = \int_0^\infty t^{a-1} e^{-t} \, dt$$

There's a useful relationship between the beta and gamma functions. The hint tells us to use the property:

$$\Gamma(a+1) = a\Gamma(a)$$

This is the recursive property of the gamma function, which you probably know from $n! = n \cdot (n-1)!$ for integers.

---

### Step 3: Use a Key Integral Identity

There's a classical result that connects the beta function to gamma functions:

$$B(a,b) = \frac{\Gamma(a)\Gamma(b)}{\Gamma(a+b)}$$

To derive this, we can use the integral representation of the gamma function and make a substitution. Here's the idea:

1. Write $\Gamma(a)$ and $\Gamma(b)$ as integrals:
   $$\Gamma(a) = \int_0^\infty s^{a-1} e^{-s} \, ds$$
   $$\Gamma(b) = \int_0^\infty t^{b-1} e^{-t} \, dt$$

2. Multiply them together:
   $$\Gamma(a)\Gamma(b) = \int_0^\infty \int_0^\infty s^{a-1} t^{b-1} e^{-(s+t)} \, ds \, dt$$

3. Make the substitution $u = s + t$ and $x = \frac{s}{s+t}$, so $s = ux$ and $t = u(1-x)$.

4. The Jacobian of this transformation is $u$, and the limits become $0 \leq x \leq 1$ and $0 \leq u < \infty$.

5. After substitution, the double integral separates into:
   $$\Gamma(a)\Gamma(b) = \left(\int_0^1 x^{a-1}(1-x)^{b-1} \, dx\right) \left(\int_0^\infty u^{a+b-1} e^{-u} \, du\right)$$

6. Recognize that:
   - The first integral is $B(a,b)$
   - The second integral is $\Gamma(a+b)$

So we get:
$$\Gamma(a)\Gamma(b) = B(a,b) \cdot \Gamma(a+b)$$

Rearranging:
$$B(a,b) = \frac{\Gamma(a)\Gamma(b)}{\Gamma(a+b)}$$

---

### Step 4: Therefore, the Normalizing Constant is...

The normalizing constant in the beta PDF is:

$$\frac{1}{B(a,b)} = \frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)}$$

This is exactly what we wanted to show! ✅

---

### Why This Matters

This result is crucial in Bayesian statistics. The beta distribution is the **conjugate prior** for the Bernoulli and binomial likelihoods. When you're doing Bayesian A/B testing or parameter estimation for probabilities, you constantly work with beta distributions.

Knowing that the normalizing constant is expressed in terms of gamma functions makes it easy to:
- Compute posterior distributions analytically
- Derive moments (mean, variance)
- Work with the beta-binomial distribution

If you've ever used a Bayesian framework for conversion rate optimization or click-through rate modeling, you've relied on this relationship without even thinking about it.

---

### Quick Sanity Check

For integer values, $\Gamma(n) = (n-1)!$, so if $a = 2$ and $b = 3$:

$$B(2,3) = \frac{\Gamma(2)\Gamma(3)}{\Gamma(5)} = \frac{1! \cdot 2!}{4!} = \frac{2}{24} = \frac{1}{12}$$

You can verify this by integrating $\int_0^1 x(1-x)^2 \, dx$ directly, and you'll get $\frac{1}{12}$. ✅

---

That's it for today! Next up: gamma distribution moments (Problem 2.6), which will be another fun one.
