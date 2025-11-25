---
layout: post
title: "Completeness and Uniqueness of MVU Estimators"
date: 2025-11-22
categories: [statistical-inference, estimation]
tags: [completeness, mvu-estimator, lehmann-scheffe, sufficiency]
math: true
---

If you've studied estimation theory, you've probably heard that "complete sufficient statistics lead to unique MVU estimators." Let's actually prove why.

## Definitions

A family of distributions $\{p(\mathcal{D}; \theta) : \theta \in \mathcal{A}\}$ is called **complete** if, for any vector function $h(\mathcal{D})$ such that:

$$\mathbb{E}_\mathcal{D}[h(\mathcal{D})] = \mathbf{0}, \, \forall \theta$$

we must have $h = \mathbf{0}$ almost everywhere.

In other words, the only function with zero expectation under all parameter values is the zero function itself. This is a strong condition.

## The Claim

Suppose the family is complete and there exists an MVU (minimum variance unbiased) estimator $\hat{\theta}$. Then this estimator is **unique**.

## The Proof

Assume for contradiction that there are two different MVU estimators, $\hat{\theta}_1$ and $\hat{\theta}_2$, both unbiased:

$$\mathbb{E}[\hat{\theta}_1] = \theta, \quad \mathbb{E}[\hat{\theta}_2] = \theta$$

Now define their difference:

$$h(\mathcal{D}) = \hat{\theta}_1(\mathcal{D}) - \hat{\theta}_2(\mathcal{D})$$

Since both estimators are unbiased:

$$\mathbb{E}[h(\mathcal{D})] = \mathbb{E}[\hat{\theta}_1] - \mathbb{E}[\hat{\theta}_2] = \theta - \theta = 0$$

This holds for all $\theta \in \mathcal{A}$. But the family is complete, so by definition, the only function with zero expectation everywhere is the zero function. Therefore:

$$h(\mathcal{D}) = 0 \quad \text{almost everywhere}$$

Which means:

$$\hat{\theta}_1(\mathcal{D}) = \hat{\theta}_2(\mathcal{D}) \quad \text{almost everywhere}$$

So the two estimators are actually the same (up to a set of measure zero). This proves uniqueness.

The key insight is that completeness is a very restrictive property. It forces any zero-expectation function to be identically zero, which rules out the possibility of having two distinct unbiased estimators with the same variance. In practice, exponential families (like Gaussian, Poisson, Binomial) often satisfy completeness, which is why the Lehmann-Scheffé theorem works so well for them.
