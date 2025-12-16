---
layout: post
title: "If an Efficient Estimator Exists, It Is ML Optimal"
date: 2025-12-12
categories: [statistical-inference, estimation-theory]
tags: [efficient-estimator, maximum-likelihood, cramer-rao, fisher-information, mvue]
math: true
---

There's a beautiful connection between two seemingly different notions of optimality in estimation theory. One comes from the variance perspective—the **efficient estimator** achieves the Cramér–Rao lower bound. The other comes from the likelihood perspective—the **maximum likelihood (ML) estimator** maximizes the probability of the observed data. It turns out these two notions are not just related; when an efficient estimator exists, it *must* be the ML estimator.

This post proves that claim and unpacks why it's true.

---

## Setting the stage

Suppose we observe data $\mathbf{x} = (x_1, \ldots, x_n)$ drawn from a distribution with pdf $p(\mathbf{x}; \theta)$, where $\theta$ is an unknown scalar parameter. We're looking for an estimator $\hat{\theta}(\mathbf{x})$ that is:

1. **Unbiased:** $\mathbb{E}[\hat{\theta}] = \theta$.
2. **Efficient:** Its variance achieves the Cramér–Rao lower bound (CRLB).

Recall that the CRLB states

$$\text{Var}(\hat{\theta}) \geq \frac{1}{I(\theta)},$$

where $I(\theta)$ is the Fisher information. An estimator is called **efficient** if equality holds.

---

## The key lemma: when does equality hold?

The proof of the CRLB uses the Cauchy–Schwarz inequality. Equality in Cauchy–Schwarz occurs if and only if the two random variables involved are linearly related. Tracing through the CRLB derivation, one finds that an efficient estimator exists if and only if the score function can be written as

$$\frac{\partial \log p(\mathbf{x}; \theta)}{\partial \theta} = I(\theta) \bigl( \hat{\theta}(\mathbf{x}) - \theta \bigr).$$

This is the critical structural condition. Let's call it the **efficiency condition**.

---

## Connecting to maximum likelihood

The ML estimator $\hat{\theta}_{\text{ML}}$ is defined as the value that maximizes $\log p(\mathbf{x}; \theta)$, or equivalently, the solution to

$$\frac{\partial \log p(\mathbf{x}; \theta)}{\partial \theta} \bigg|_{\theta = \hat{\theta}_{\text{ML}}} = 0.$$

Now suppose an efficient estimator $\hat{\theta}_{\text{eff}}$ exists. By the efficiency condition,

$$\frac{\partial \log p(\mathbf{x}; \theta)}{\partial \theta} = I(\theta) \bigl( \hat{\theta}_{\text{eff}}(\mathbf{x}) - \theta \bigr).$$

Setting the left-hand side to zero and solving for $\theta$:

$$0 = I(\theta) \bigl( \hat{\theta}_{\text{eff}}(\mathbf{x}) - \theta \bigr).$$

Since $I(\theta) > 0$ for a regular family, we must have

$$\theta = \hat{\theta}_{\text{eff}}(\mathbf{x}).$$

But this equation says: the value of $\theta$ that sets the score to zero is exactly $\hat{\theta}_{\text{eff}}(\mathbf{x})$. That's precisely the definition of the ML estimator. Therefore,

$$\hat{\theta}_{\text{ML}} = \hat{\theta}_{\text{eff}}.$$

---

## What this result really says

The theorem has a satisfying interpretation:

- **Efficient estimators are rare.** Most models don't admit one.
- **When one exists, it's unique** (among unbiased estimators) and achieves the best possible variance.
- **ML automatically finds it.** You don't need to hunt for the MVUE separately; just compute the MLE.

In some sense, this justifies the popularity of maximum likelihood. When the "perfect" estimator exists, ML delivers it without requiring you to verify efficiency conditions explicitly.

---

## A concrete example

Consider $x_1, \ldots, x_n \overset{\text{iid}}{\sim} \mathcal{N}(\mu, \sigma^2)$ with $\sigma^2$ known. The sample mean

$$\hat{\mu} = \frac{1}{n} \sum_{i=1}^n x_i$$

is unbiased with variance $\sigma^2/n$. The Fisher information for $\mu$ is $I(\mu) = n/\sigma^2$, so the CRLB is $\sigma^2/n$. The sample mean achieves this bound—it's efficient.

And indeed, maximizing the log-likelihood

$$\log p(\mathbf{x}; \mu) = -\frac{n}{2}\log(2\pi\sigma^2) - \frac{1}{2\sigma^2}\sum_{i=1}^n (x_i - \mu)^2$$

with respect to $\mu$ gives exactly $\hat{\mu} = \bar{x}$. The efficient estimator and the ML estimator coincide, as the theorem guarantees.

---

## Remarks

- The converse is **not** true in general: the MLE is not always efficient, especially in finite samples.
- Asymptotically, under regularity conditions, the MLE *is* efficient—but that's a different (and weaker) statement.
- This result applies to the scalar parameter case. For vector parameters, the analogous statement involves the full Fisher information matrix and is more delicate.

The theorem we proved here is the strong, finite-sample version: if an efficient estimator exists, ML finds it exactly.
