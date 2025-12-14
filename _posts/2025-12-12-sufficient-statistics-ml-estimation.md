---
title: "Why Sufficient Statistics Are All You Need for Maximum Likelihood"
date: "2025-12-12"
slug: "sufficient-statistics-ml-estimation"
description: "Proving that if a sufficient statistic exists, the ML estimate can be expressed as a function of that statistic alone—no need to look at the full data."
tags: ["statistics", "sufficient statistics", "maximum likelihood", "estimation theory", "factorization theorem"]
---

There's a beautiful economy principle hiding in estimation theory: if you've found a sufficient statistic, you've found everything that matters for maximum likelihood estimation.

This isn't just an elegant mathematical curiosity—it has profound practical implications. It tells us that data compression, when done correctly, costs us nothing in terms of estimation quality.

## The Claim

Let $T(\mathcal{X})$ be a sufficient statistic for parameter $\theta$. Then the maximum likelihood estimate $\hat{\theta}_{\text{ML}}$ can be written purely as a function of $T(\mathcal{X})$.

In other words:
\[
\hat{\theta}_{\text{ML}} = g(T(\mathcal{X}))
\]
for some function $g$.

## What Sufficiency Gives Us

By the Fisher-Neyman factorization theorem, $T(\mathcal{X})$ is sufficient for $\theta$ if and only if the likelihood function factors as:
\[
L(\theta; \mathcal{X}) = h(\mathcal{X}) \cdot g(T(\mathcal{X}), \theta)
\]

Here $h(\mathcal{X})$ depends only on the data (not on $\theta$), while $g(T(\mathcal{X}), \theta)$ captures all the $\theta$-dependence through the sufficient statistic.

## The Proof

The ML estimate maximizes the likelihood:
\[
\hat{\theta}_{\text{ML}} = \arg\max_{\theta} \, L(\theta; \mathcal{X})
\]

Substituting the factorization:
\[
\hat{\theta}_{\text{ML}} = \arg\max_{\theta} \, h(\mathcal{X}) \cdot g(T(\mathcal{X}), \theta)
\]

Now here's the key observation: $h(\mathcal{X}) \geq 0$ (it's part of a probability density), and crucially, **it doesn't depend on $\theta$**.

So when we're maximizing over $\theta$, the factor $h(\mathcal{X})$ is just a positive constant. It doesn't affect where the maximum occurs:
\[
\hat{\theta}_{\text{ML}} = \arg\max_{\theta} \, g(T(\mathcal{X}), \theta)
\]

And there it is. The right-hand side depends on $\mathcal{X}$ only through $T(\mathcal{X})$.

Define:
\[
\hat{\theta}_{\text{ML}} = \psi(T(\mathcal{X})) \quad \text{where} \quad \psi(t) = \arg\max_{\theta} \, g(t, \theta)
\]

The ML estimate is a function of the sufficient statistic alone. $\blacksquare$

## Remarks

- **Data reduction without loss**: This result justifies why we can "compress" data into sufficient statistics before doing ML estimation. We lose no information relevant to finding the optimal $\theta$.

- **Computational blessing**: In practice, sufficient statistics are often low-dimensional summaries. Instead of maximizing over the full data space, we work with these summaries—same answer, less computation.

- **The converse intuition**: This result makes sense when you think about what sufficiency means. If $T(\mathcal{X})$ captures everything the data tells us about $\theta$, then of course our best guess about $\theta$ shouldn't need anything beyond $T(\mathcal{X})$.

- **Connection to exponential families**: For exponential family distributions, the sufficient statistic has a particularly nice form, and ML estimation often reduces to simple moment matching with $T(\mathcal{X})$.

- **Why $h(\mathcal{X}) \geq 0$ matters**: We used that $h$ is non-negative. If $h$ could be negative, multiplying by it might flip the optimization. But since $h$ is part of factoring a density, non-negativity is guaranteed.
