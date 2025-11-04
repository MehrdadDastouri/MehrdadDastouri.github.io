---
layout: post
title: "Deriving the Covariance Matrix for Multivariate Gaussian"
date: 2025-11-04 08:00:00 -0400
categories: statistics probability
tags: math multivariate-gaussian covariance-matrix linear-algebra
---

I've been working with Gaussian distributions for a while now, but I realized I'd never actually sat down and derived the covariance matrix for the multivariate case from first principles. It's one of those things you see everywhere in ML – from Gaussian Mixture Models to Kalman filters to variational inference – but the derivation felt like muscle memory at this point rather than real understanding.

Time to fix that.

## The Multivariate Gaussian

A random vector $\mathbf{x} \in \mathbb{R}^n$ follows a multivariate Gaussian distribution $\mathcal{N}(\boldsymbol{\mu}, \boldsymbol{\Sigma})$ with PDF:

$$ f(\mathbf{x}) = \frac{1}{(2\pi)^{n/2} |\boldsymbol{\Sigma}|^{1/2}} \exp\left(-\frac{1}{2}(\mathbf{x} - \boldsymbol{\mu})^\top \boldsymbol{\Sigma}^{-1} (\mathbf{x} - \boldsymbol{\mu})\right) $$

Here, $\boldsymbol{\mu}$ is the mean vector and $\boldsymbol{\Sigma}$ is the covariance matrix. The goal is to show that $\boldsymbol{\Sigma}$ is actually the covariance matrix in the statistical sense:

$$ \boldsymbol{\Sigma}_{ij} = \text{Cov}(x_i, x_j) = E[(x_i - \mu_i)(x_j - \mu_j)] $$

---

## Mean Vector

First, let me confirm the mean. For component $x_i$:

$$ E[x_i] = \int_{\mathbb{R}^n} x_i \cdot f(\mathbf{x}) \, d\mathbf{x} $$

By symmetry of the Gaussian and the fact that the distribution is centered at $\boldsymbol{\mu}$, we have:

$$ E[\mathbf{x}] = \boldsymbol{\mu} $$

This one's straightforward – the distribution is literally centered at $\boldsymbol{\mu}$.

---

## Covariance Matrix

Now for the interesting part. The covariance matrix is defined as:

$$ \boldsymbol{\Sigma} = E[(\mathbf{x} - \boldsymbol{\mu})(\mathbf{x} - \boldsymbol{\mu})^\top] $$

Let $\mathbf{y} = \mathbf{x} - \boldsymbol{\mu}$ be the centered random vector. Then:

$$ \boldsymbol{\Sigma} = E[\mathbf{y}\mathbf{y}^\top] $$

The $(i,j)$-th element is:

$$ \Sigma_{ij} = E[y_i y_j] = \int_{\mathbb{R}^n} y_i y_j \cdot f(\mathbf{x}) \, d\mathbf{x} $$

Substitute the PDF (with $\mathbf{y} = \mathbf{x} - \boldsymbol{\mu}$):

$$ \Sigma_{ij} = \frac{1}{(2\pi)^{n/2} |\boldsymbol{\Sigma}|^{1/2}} \int_{\mathbb{R}^n} y_i y_j \exp\left(-\frac{1}{2}\mathbf{y}^\top \boldsymbol{\Sigma}^{-1} \mathbf{y}\right) d\mathbf{y} $$

Here's the trick: use a change of variables. Let $\mathbf{z} = \boldsymbol{\Sigma}^{-1/2} \mathbf{y}$, where $\boldsymbol{\Sigma}^{-1/2}$ is the matrix square root (via eigendecomposition). Then $\mathbf{y} = \boldsymbol{\Sigma}^{1/2} \mathbf{z}$ and $d\mathbf{y} = |\boldsymbol{\Sigma}|^{1/2} d\mathbf{z}$.

The quadratic form becomes:

$$ \mathbf{y}^\top \boldsymbol{\Sigma}^{-1} \mathbf{y} = \mathbf{z}^\top \mathbf{z} = \|\mathbf{z}\|^2 $$

So the integral transforms to:

$$ \Sigma_{ij} = \frac{1}{(2\pi)^{n/2}} \int_{\mathbb{R}^n} (\boldsymbol{\Sigma}^{1/2}\mathbf{z})_i (\boldsymbol{\Sigma}^{1/2}\mathbf{z})_j \exp\left(-\frac{1}{2}\|\mathbf{z}\|^2\right) d\mathbf{z} $$

Write $(\boldsymbol{\Sigma}^{1/2})_{ik}$ as the $(i,k)$-th element:

$$ (\boldsymbol{\Sigma}^{1/2}\mathbf{z})_i = \sum_k (\boldsymbol{\Sigma}^{1/2})_{ik} z_k $$

So:

$$ \Sigma_{ij} = \sum_{k,\ell} (\boldsymbol{\Sigma}^{1/2})_{ik} (\boldsymbol{\Sigma}^{1/2})_{j\ell} \cdot \frac{1}{(2\pi)^{n/2}} \int_{\mathbb{R}^n} z_k z_\ell \exp\left(-\frac{1}{2}\|\mathbf{z}\|^2\right) d\mathbf{z} $$

The integral is just $E[z_k z_\ell]$ under the standard multivariate Gaussian $\mathcal{N}(0, I)$. Since components are independent:

$$ E[z_k z_\ell] = \begin{cases} 1 & \text{if } k = \ell \\ 0 & \text{if } k \neq \ell \end{cases} = \delta_{k\ell} $$

So:

$$ \Sigma_{ij} = \sum_{k} (\boldsymbol{\Sigma}^{1/2})_{ik} (\boldsymbol{\Sigma}^{1/2})_{jk} = (\boldsymbol{\Sigma}^{1/2} (\boldsymbol{\Sigma}^{1/2})^\top)_{ij} $$

But $\boldsymbol{\Sigma}^{1/2} (\boldsymbol{\Sigma}^{1/2})^\top = \boldsymbol{\Sigma}$ by definition of the matrix square root.

$$ \boxed{\boldsymbol{\Sigma}_{ij} = \text{Cov}(x_i, x_j)} $$

---

## Why This Matters

This derivation confirms that the $\boldsymbol{\Sigma}$ parameter in the multivariate Gaussian PDF is *exactly* the covariance matrix. It's not just notation – it's the actual second moment structure of the distribution.

In practice, I see this constantly when fitting Gaussian models. The eigenvalues of $\boldsymbol{\Sigma}$ give the variance along principal components, and the eigenvectors give the axes of the ellipsoid. When $\boldsymbol{\Sigma}$ is diagonal, the components are uncorrelated (and for Gaussians, that means independent).

This also explains why $\boldsymbol{\Sigma}$ must be positive semidefinite – it's a covariance matrix. Any violation of that would break the math and make the distribution non-normalizable.

I run into this constantly when debugging Gaussian Mixture Models or implementing Kalman filters. If the covariance matrix isn't positive definite, the whole thing collapses.
