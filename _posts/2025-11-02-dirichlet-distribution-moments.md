---
layout: post
title: "Exploring the Dirichlet Distribution: A Journey Through Its Moments"
date: 2025-11-02 09:00:00 -0400
categories: statistics probability
tags: math multivariate-statistics dirichlet-distribution
---

So, after spending some time with the Beta distribution (which I wrote about earlier), I kept thinking about what comes next. The Beta distribution is great for modeling proportions between two outcomes, but what if we have more than two categories? That's where the Dirichlet distribution comes in – it's basically the Beta distribution's cooler, multidimensional cousin.

## What is the Dirichlet Distribution?

The Dirichlet distribution is parameterized by a vector of positive values $\mathbf{a} = (a_1, a_2, \dots, a_K)$. If you're doing Bayesian inference with categorical or multinomial data, you've probably encountered it as a conjugate prior. It's incredibly useful for that.

A random vector $\mathbf{x} = (x_1, \dots, x_K)$ follows a Dirichlet distribution (we write $\mathbf{x} \sim \text{Dir}(\mathbf{a})$) when it lives on the simplex – meaning each component is positive and they all sum to 1. The PDF looks like this:

$$ f(\mathbf{x}; \mathbf{a}) = \frac{\Gamma(\bar{a})}{\prod_{k=1}^K \Gamma(a_k)} \prod_{k=1}^K x_k^{a_k-1} $$

where I'm using $\bar{a} = \sum_{k=1}^K a_k$ for convenience. That $\Gamma(\bar{a}) / \prod_{k=1}^K \Gamma(a_k)$ term is just the normalization constant (the multivariate Beta function).

Today I want to work through the moments of this distribution. Specifically, I'll derive the mean, variance, and covariance. These calculations come up all the time in practice, and understanding where they come from gives you better intuition about how the Dirichlet behaves.

---

## Finding the Mean

Let's start with the expected value of some component $x_k$. We need to integrate $x_k$ times the PDF over the simplex:

$$ E[x_k] = \int_{\mathcal{S}_K} x_k \cdot f(\mathbf{x}; \mathbf{a}) \,d\mathbf{x} $$

Pulling out the constant and absorbing $x_k$ into the product:

$$ E[x_k] = \frac{\Gamma(\bar{a})}{\prod_{j=1}^K \Gamma(a_j)} \int_{\mathcal{S}_K} x_k^{a_k} \prod_{j \neq k} x_j^{a_j-1} \,d\mathbf{x} $$

Here's the trick: that integral is almost another Dirichlet! If we define new parameters where $a'_k = a_k+1$ and keep everything else the same, then $\bar{a}' = \bar{a}+1$, and we recognize the integral as:

$$ \int_{\mathcal{S}_K} \prod_{j=1}^K x_j^{a'_j-1} \,d\mathbf{x} = \frac{\Gamma(a_k+1) \prod_{j \neq k} \Gamma(a_j)}{\Gamma(\bar{a}+1)} $$

Now we substitute back and use the fact that $\Gamma(z+1) = z\Gamma(z)$:

$$ E[x_k] = \frac{\Gamma(\bar{a})}{\prod_{j=1}^K \Gamma(a_j)} \cdot \frac{\Gamma(a_k+1) \prod_{j \neq k} \Gamma(a_j)}{\Gamma(\bar{a}+1)} = \frac{a_k}{\bar{a}} $$

Pretty clean! The mean is just the component's parameter divided by the sum of all parameters.

$$ \boxed{E[x_k] = \frac{a_k}{\bar{a}}} $$

---

## Second Moments: Setting Up for Variance and Covariance

To get variance and covariance, we need second moments. Let me work through both $E[x_k^2]$ and $E[x_i x_j]$.

**For the squared term $E[x_k^2]$:**

Using the same approach:

$$ E[x_k^2] = \frac{\Gamma(\bar{a})}{\prod_{j=1}^K \Gamma(a_j)} \int_{\mathcal{S}_K} x_k^{a_k+1} \prod_{j \neq k} x_j^{a_j-1} \,d\mathbf{x} $$

This time we're bumping $a_k$ up by 2, so the sum becomes $\bar{a}+2$. The integral evaluates to:

$$ \frac{\Gamma(a_k+2) \prod_{j \neq k} \Gamma(a_j)}{\Gamma(\bar{a}+2)} $$

Simplifying with the recursion property of the Gamma function:

$$ E[x_k^2] = \frac{\Gamma(\bar{a})}{\Gamma(a_k)} \cdot \frac{(a_k+1)a_k\Gamma(a_k)}{(\bar{a}+1)\bar{a}\Gamma(\bar{a})} = \frac{a_k(a_k+1)}{\bar{a}(\bar{a}+1)} $$

**For the cross term $E[x_i x_j]$ where $i \neq j$:**

$$ E[x_i x_j] = \frac{\Gamma(\bar{a})}{\prod_{k=1}^K \Gamma(a_k)} \int_{\mathcal{S}_K} x_i^{a_i} x_j^{a_j} \prod_{k \neq i,j} x_k^{a_k-1} \,d\mathbf{x} $$

Here both $a_i$ and $a_j$ get incremented, still giving us $\bar{a}+2$:

$$ E[x_i x_j] = \frac{\Gamma(\bar{a})}{\Gamma(a_i)\Gamma(a_j)} \cdot \frac{a_i\Gamma(a_i)a_j\Gamma(a_j)}{(\bar{a}+1)\bar{a}\Gamma(\bar{a})} = \frac{a_i a_j}{\bar{a}(\bar{a}+1)} $$

---

## Putting It Together: Variance and Covariance

Now we just use the standard formulas: $\text{Var}(X) = E[X^2] - (E[X])^2$ and $\text{Cov}(X,Y) = E[XY] - E[X]E[Y]$.

**Variance:**

$$ \text{Var}(x_k) = \frac{a_k(a_k+1)}{\bar{a}(\bar{a}+1)} - \left(\frac{a_k}{\bar{a}}\right)^2 $$

Getting a common denominator and simplifying:

$$ \text{Var}(x_k) = \frac{a_k(a_k+1)\bar{a} - a_k^2(\bar{a}+1)}{\bar{a}^2(\bar{a}+1)} = \frac{a_k\bar{a} - a_k^2}{\bar{a}^2(\bar{a}+1)} $$

$$ \boxed{\sigma_{x_k}^2 = \frac{a_k(\bar{a}-a_k)}{\bar{a}^2(\bar{a}+1)}} $$

**Covariance:**

$$ \text{Cov}(x_i, x_j) = \frac{a_i a_j}{\bar{a}(\bar{a}+1)} - \frac{a_i}{\bar{a}} \cdot \frac{a_j}{\bar{a}} $$

$$ = \frac{a_i a_j \bar{a} - a_i a_j(\bar{a}+1)}{\bar{a}^2(\bar{a}+1)} = \frac{-a_i a_j}{\bar{a}^2(\bar{a}+1)} $$

$$ \boxed{\text{Cov}(x_i, x_j) = -\frac{a_i a_j}{\bar{a}^2(\bar{a}+1)}} $$

Notice that negative covariance! This makes sense – if the components must sum to 1, then when one goes up, others must go down. The Dirichlet naturally captures this constraint.

---

## Wrapping Up

Working through these derivations gave me a much better feel for how the Dirichlet works. The parameters $a_k$ control not just the mean of each component, but also how concentrated the distribution is around that mean. When you see $\bar{a}$ in the denominators of the variance and covariance, you can think of it as a "concentration parameter" – larger values mean tighter concentration around the mean.

These formulas come up constantly when working with topic models, Bayesian mixture models, or any time you're putting priors on probability vectors. Worth keeping in your back pocket!
