---
layout: post
title: "Deriving the Normal Equation for Linear Regression"
date: 2025-10-27 11:00:00 -0400
categories: machine-learning mathematics linear-regression
---

Linear regression is probably the first ML algorithm I ever learned, and I've implemented it dozens of times. But recently I caught myself just calling `model.fit()` without really thinking about what's happening under the hood. So I sat down and worked through the Normal Equation derivation from scratch.

Turns out there's some genuinely elegant calculus here. It's one of those rare cases where the math is both clean *and* intuitive.

## The Goal

Find the parameter vector $\boldsymbol{\theta}$ that minimizes squared error. For a single data point $\mathbf{x}_n$, our prediction is:

$$ \hat{y}_n = \boldsymbol{\theta}^T \mathbf{x}_n $$

Simple enough. Now minimize the total error.

---

## The Cost Function

Sum of squared errors across all $N$ points:

$$ J(\boldsymbol{\theta}) = \sum_{n=1}^{N} (y_n - \boldsymbol{\theta}^T \mathbf{x}_n)^2 $$

We square errors so positive and negative deviations don't cancel. Also penalizes large mistakes more heavily, which usually makes sense.

## Matrix Form (Way Cleaner)

Summations get messy fast. Let me use matrix notation:

- $\mathbf{y}$: target values $[y_1, y_2, \dots, y_N]^T$
- $\mathbf{X}$: design matrix (each row is $\mathbf{x}_n^T$)
- $\boldsymbol{\theta}$: parameter vector

Cost function becomes:

$$ J(\boldsymbol{\theta}) = \| \mathbf{y} - \mathbf{X}\boldsymbol{\theta} \|_2^2 = (\mathbf{y} - \mathbf{X}\boldsymbol{\theta})^T (\mathbf{y} - \mathbf{X}\boldsymbol{\theta}) $$

Much better.

---

## Finding the Minimum

Expand it out:

$$ J(\boldsymbol{\theta}) = (\mathbf{y}^T - \boldsymbol{\theta}^T\mathbf{X}^T) (\mathbf{y} - \mathbf{X}\boldsymbol{\theta}) $$

$$ = \mathbf{y}^T\mathbf{y} - \mathbf{y}^T\mathbf{X}\boldsymbol{\theta} - \boldsymbol{\theta}^T\mathbf{X}^T\mathbf{y} + \boldsymbol{\theta}^T\mathbf{X}^T\mathbf{X}\boldsymbol{\theta} $$

Here's a nice trick: $\boldsymbol{\theta}^T\mathbf{X}^T\mathbf{y}$ is a scalar, so it equals its transpose. Combine those middle terms:

$$ J(\boldsymbol{\theta}) = \mathbf{y}^T\mathbf{y} - 2\boldsymbol{\theta}^T\mathbf{X}^T\mathbf{y} + \boldsymbol{\theta}^T\mathbf{X}^T\mathbf{X}\boldsymbol{\theta} $$

Take the gradient:

$$ \nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta}) = -2\mathbf{X}^T\mathbf{y} + 2\mathbf{X}^T\mathbf{X}\boldsymbol{\theta} $$

Set it to zero:

$$ -2\mathbf{X}^T\mathbf{y} + 2\mathbf{X}^T\mathbf{X}\hat{\boldsymbol{\theta}} = \mathbf{0} $$

$$ \boxed{\mathbf{X}^T\mathbf{X}\hat{\boldsymbol{\theta}} = \mathbf{X}^T\mathbf{y}} $$

That's the Normal Equation. If $\mathbf{X}^T\mathbf{X}$ is invertible (usually is), then:

$$ \hat{\boldsymbol{\theta}} = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y} $$

### What It Means

Sometimes the summation form makes more intuitive sense:

$$ \left(\sum_{n=1}^{N} \mathbf{x}_n \mathbf{x}_n^T\right) \hat{\boldsymbol{\theta}} = \sum_{n=1}^{N} y_n \mathbf{x}_n $$

Left side: sum of outer products of features. Right side: features weighted by targets. It's basically saying "match the weighted average of inputs to outputs."

---

## Why This Matters

I rarely compute this by hand anymore – gradient descent is often faster for large datasets, and libraries handle everything. But understanding the closed-form solution helps with:

- **Debugging**: When linear regression fails, it's usually because $\mathbf{X}^T\mathbf{X}$ is singular (collinear features)
- **Regularization**: Ridge regression just adds $\lambda \mathbf{I}$ to $\mathbf{X}^T\mathbf{X}$, which makes perfect sense once you see this
- **Weighted least squares**: Same derivation, just add a weight matrix

Plus the matrix calculus tricks here show up *everywhere* in ML – from neural net backprop to kernel methods.

Next up: I want to dig into the Beta and Dirichlet distributions. They're conjugate priors for binomial and multinomial likelihoods, and there's some really satisfying math connecting everything together.
