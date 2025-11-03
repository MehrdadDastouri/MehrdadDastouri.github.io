---
layout: post
title: "Dirichlet Distribution Moments: From Beta to Multiple Categories"
date: 2025-11-02 09:00:00 -0400
categories: statistics probability
tags: math multivariate-statistics dirichlet-distribution
---

After working through the Beta distribution, I kept wondering: what happens when you have *more* than two categories? Turns out there's a natural extension called the Dirichlet distribution, and it shows up everywhere in Bayesian methods – topic models, mixture models, anything involving probability vectors.

I decided to derive the mean, variance, and covariance myself. The algebra gets a bit messier than the Beta case, but the structure is really satisfying.

## The Dirichlet Distribution

A random vector $\mathbf{x} = (x_1, \dots, x_K)$ follows $\text{Dir}(\mathbf{a})$ where $\mathbf{a} = (a_1, \dots, a_K)$ are positive parameters. The components live on the simplex: $x_k > 0$ and $\sum_k x_k = 1$.

PDF:

$$ f(\mathbf{x}; \mathbf{a}) = \frac{\Gamma(\bar{a})}{\prod_{k=1}^K \Gamma(a_k)} \prod_{k=1}^K x_k^{a_k-1} $$

I'm using $\bar{a} = \sum_{k=1}^K a_k$ as shorthand. That big fraction up front is the normalization constant (multivariate Beta function).

If you've done Bayesian inference with categorical data, you've probably used this as a conjugate prior for the multinomial distribution. It's the go-to choice.

---

## Mean

Start with: $E[x_k] = \int_{\mathcal{S}_K} x_k \cdot f(\mathbf{x}; \mathbf{a}) \,d\mathbf{x}$

Pull out constants and absorb $x_k$:

$$ E[x_k] = \frac{\Gamma(\bar{a})}{\prod_{j=1}^K \Gamma(a_j)} \int_{\mathcal{S}_K} x_k^{a_k} \prod_{j \neq k} x_j^{a_j-1} \,d\mathbf{x} $$

That integral? It's another Dirichlet with parameters $(a_1, \dots, a_k+1, \dots, a_K)$ and sum $\bar{a}+1$:

$$ \int_{\mathcal{S}_K} \prod_{j=1}^K x_j^{a'_j-1} \,d\mathbf{x} = \frac{\Gamma(a_k+1) \prod_{j \neq k} \Gamma(a_j)}{\Gamma(\bar{a}+1)} $$

Substitute back, use $\Gamma(z+1) = z\Gamma(z)$:

$$ E[x_k] = \frac{\Gamma(\bar{a})}{\prod_{j} \Gamma(a_j)} \cdot \frac{\Gamma(a_k+1) \prod_{j \neq k} \Gamma(a_j)}{\Gamma(\bar{a}+1)} = \frac{a_k\Gamma(a_k)}{\bar{a}\Gamma(\bar{a})} \cdot \frac{\Gamma(\bar{a})}{\Gamma(a_k)} = \frac{a_k}{\bar{a}} $$

$$ \boxed{E[x_k] = \frac{a_k}{\bar{a}}} $$

Clean! Each component's mean is just its parameter relative to the total.

---

## Second Moments

Need $E[x_k^2]$ and $E[x_i x_j]$ to get variance and covariance.

**For $E[x_k^2]$:**

$$ E[x_k^2] = \frac{\Gamma(\bar{a})}{\prod_{j} \Gamma(a_j)} \int_{\mathcal{S}_K} x_k^{a_k+1} \prod_{j \neq k} x_j^{a_j-1} \,d\mathbf{x} $$

Bump $a_k$ by 2, so $\bar{a} \to \bar{a}+2$:

$$ E[x_k^2] = \frac{\Gamma(\bar{a})}{\Gamma(a_k)} \cdot \frac{\Gamma(a_k+2)}{\Gamma(\bar{a}+2)} = \frac{a_k(a_k+1)}{\bar{a}(\bar{a}+1)} $$

**For $E[x_i x_j]$ where $i \neq j$:**

$$ E[x_i x_j] = \frac{\Gamma(\bar{a})}{\prod_k \Gamma(a_k)} \int_{\mathcal{S}_K} x_i^{a_i} x_j^{a_j} \prod_{k \neq i,j} x_k^{a_k-1} \,d\mathbf{x} $$

Both $a_i$ and $a_j$ increment:

$$ E[x_i x_j] = \frac{\Gamma(\bar{a})}{\Gamma(a_i)\Gamma(a_j)} \cdot \frac{a_i\Gamma(a_i) \cdot a_j\Gamma(a_j)}{(\bar{a}+1)\bar{a}\Gamma(\bar{a})} = \frac{a_i a_j}{\bar{a}(\bar{a}+1)} $$

---

## Variance and Covariance

Use $\text{Var}(X) = E[X^2] - (E[X])^2$ and $\text{Cov}(X,Y) = E[XY] - E[X]E[Y]$.

**Variance:**

$$ \text{Var}(x_k) = \frac{a_k(a_k+1)}{\bar{a}(\bar{a}+1)} - \left(\frac{a_k}{\bar{a}}\right)^2 $$

Common denominator:

$$ = \frac{a_k(a_k+1)\bar{a} - a_k^2(\bar{a}+1)}{\bar{a}^2(\bar{a}+1)} = \frac{a_k^2\bar{a} + a_k\bar{a} - a_k^2\bar{a} - a_k^2}{\bar{a}^2(\bar{a}+1)} $$

$$ \boxed{\sigma_{x_k}^2 = \frac{a_k(\bar{a}-a_k)}{\bar{a}^2(\bar{a}+1)}} $$

**Covariance:**

$$ \text{Cov}(x_i, x_j) = \frac{a_i a_j}{\bar{a}(\bar{a}+1)} - \frac{a_i a_j}{\bar{a}^2} $$

$$ = \frac{a_i a_j \bar{a} - a_i a_j(\bar{a}+1)}{\bar{a}^2(\bar{a}+1)} $$

$$ \boxed{\text{Cov}(x_i, x_j) = -\frac{a_i a_j}{\bar{a}^2(\bar{a}+1)}} $$

Negative covariance! Makes total sense – components sum to 1, so if one increases, others must decrease. The Dirichlet enforces this constraint automatically.

---

## Takeaways

The parameter $\bar{a}$ acts like a concentration parameter. Larger $\bar{a}$ means smaller variance and covariance – the distribution gets tighter around the mean. You see this pattern everywhere: topic models (LDA), Bayesian mixture models, anywhere you're modeling probability vectors.

When I'm setting priors in practice, I usually start with symmetric Dirichlet (all $a_k$ equal). Small values like $a_k = 0.1$ give you sparse distributions (most probability mass on a few categories). Large values like $a_k = 10$ push everything toward uniform.

These formulas come up constantly. Definitely worth having the intuition locked in.
