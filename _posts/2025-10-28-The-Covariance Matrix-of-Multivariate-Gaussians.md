---
layout: post
title: "The Covariance Matrix of Multivariate Gaussians"
date: 2025-10-28 10:00:00 -0400
categories: probability statistics
tags: math multivariate gaussian
---

I've been working with multivariate Gaussians a lot lately – they show up everywhere in ML, from Gaussian processes to variational autoencoders. But I realized I'd never actually derived why the covariance matrix has the form it does. I mean, I *use* $\boldsymbol{\Sigma}$ constantly, but where does it come from?

So I sat down and worked through the algebra. It's cleaner than I expected.

## The Setup

A random vector $\mathbf{X} \sim \mathcal{N}(\boldsymbol{\mu}, \boldsymbol{\Sigma})$ in $\mathbb{R}^n$ has PDF:

$$ f(\mathbf{x}) = \frac{1}{(2\pi)^{n/2}|\boldsymbol{\Sigma}|^{1/2}} \exp\left(-\frac{1}{2}(\mathbf{x}-\boldsymbol{\mu})^T\boldsymbol{\Sigma}^{-1}(\mathbf{x}-\boldsymbol{\mu})\right) $$

The mean vector is straightforward: $E[\mathbf{X}] = \boldsymbol{\mu}$.

But what about the covariance matrix? The definition is:

$$ \text{Cov}(\mathbf{X}) = E[(\mathbf{X} - \boldsymbol{\mu})(\mathbf{X} - \boldsymbol{\mu})^T] $$

I want to show this equals $\boldsymbol{\Sigma}$.

---

## Deriving the Mean

First, let me verify the mean. Start with:

$$ E[\mathbf{X}] = \int_{\mathbb{R}^n} \mathbf{x} \cdot f(\mathbf{x}) \, d\mathbf{x} $$

Since the Gaussian is symmetric around $\boldsymbol{\mu}$, we can shift coordinates. Let $\mathbf{y} = \mathbf{x} - \boldsymbol{\mu}$:

$$ E[\mathbf{X}] = \int_{\mathbb{R}^n} (\mathbf{y} + \boldsymbol{\mu}) \cdot \frac{1}{(2\pi)^{n/2}|\boldsymbol{\Sigma}|^{1/2}} \exp\left(-\frac{1}{2}\mathbf{y}^T\boldsymbol{\Sigma}^{-1}\mathbf{y}\right) d\mathbf{y} $$

The integral of $\mathbf{y}$ over a symmetric distribution is zero (odd function). So:

$$ E[\mathbf{X}] = \boldsymbol{\mu} \int_{\mathbb{R}^n} \frac{1}{(2\pi)^{n/2}|\boldsymbol{\Sigma}|^{1/2}} \exp\left(-\frac{1}{2}\mathbf{y}^T\boldsymbol{\Sigma}^{-1}\mathbf{y}\right) d\mathbf{y} = \boldsymbol{\mu} $$

That integral is just 1 (the PDF normalizes). ✓

---

## The Covariance Matrix

Now the interesting part. We need:

$$ \text{Cov}(\mathbf{X}) = E[(\mathbf{X} - \boldsymbol{\mu})(\mathbf{X} - \boldsymbol{\mu})^T] $$

Using the same substitution $\mathbf{y} = \mathbf{x} - \boldsymbol{\mu}$:

$$ \text{Cov}(\mathbf{X}) = \int_{\mathbb{R}^n} \mathbf{y}\mathbf{y}^T \cdot \frac{1}{(2\pi)^{n/2}|\boldsymbol{\Sigma}|^{1/2}} \exp\left(-\frac{1}{2}\mathbf{y}^T\boldsymbol{\Sigma}^{-1}\mathbf{y}\right) d\mathbf{y} $$

This is an $n \times n$ matrix. The $(i,j)$-th entry is:

$$ [\text{Cov}(\mathbf{X})]_{ij} = E[y_i y_j] $$

Here's the key insight: the quadratic form $\mathbf{y}^T\boldsymbol{\Sigma}^{-1}\mathbf{y}$ in the exponential encodes all the covariance structure.

To see this explicitly, write $\boldsymbol{\Sigma}^{-1} = \mathbf{A}$ (the precision matrix). The exponent becomes:

$$ -\frac{1}{2}\sum_{k,\ell} y_k A_{k\ell} y_\ell $$

When we compute $E[y_i y_j]$, we're essentially asking: "What's the coefficient structure that makes this Gaussian integrate to 1?"

The answer comes from a standard Gaussian integral identity. For a zero-mean Gaussian with covariance $\boldsymbol{\Sigma}$:

$$ E[y_i y_j] = \Sigma_{ij} $$

This follows from differentiating the moment-generating function, but there's a more direct way using integration by parts in multiple dimensions.

---

## The Direct Calculation (Sketch)

If you want to see it explicitly, consider the univariate case first. For $Y \sim \mathcal{N}(0, \sigma^2)$:

$$ E[Y^2] = \int_{-\infty}^{\infty} y^2 \cdot \frac{1}{\sqrt{2\pi\sigma^2}} e^{-y^2/(2\sigma^2)} dy $$

Integration by parts gives $E[Y^2] = \sigma^2$.

For the multivariate case, the same principle applies. The covariance matrix $\boldsymbol{\Sigma}$ appears naturally when you compute:

$$ \int_{\mathbb{R}^n} y_i y_j \exp\left(-\frac{1}{2}\mathbf{y}^T\boldsymbol{\Sigma}^{-1}\mathbf{y}\right) d\mathbf{y} $$

The result is:

$$ \boxed{\text{Cov}(\mathbf{X}) = \boldsymbol{\Sigma}} $$

---

## Why This Matters

Understanding this makes working with Gaussian processes way less mysterious. The covariance matrix $\boldsymbol{\Sigma}$ directly encodes how variables covary – that's not a coincidence, it's literally the definition.

When you're fitting a Gaussian mixture model or doing Kalman filtering, you're constantly estimating $\boldsymbol{\Sigma}$. Knowing it comes from $E[(\mathbf{X}-\boldsymbol{\mu})(\mathbf{X}-\boldsymbol{\mu})^T]$ makes debugging much easier.

Also, in high dimensions, $\boldsymbol{\Sigma}$ can be huge. Techniques like diagonal covariance approximations (assuming independence) or low-rank structures (factor analysis) all make sense once you see $\boldsymbol{\Sigma}$ as encoding pairwise covariances.

I've been using this in some clustering work recently, and it's wild how much cleaner the math becomes when you just embrace the matrix notation instead of trying to think component-wise.
