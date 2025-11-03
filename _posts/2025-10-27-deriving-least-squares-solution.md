---
layout: post
title: "Deriving the Mean and Variance of the Binomial Distribution"
date: 2025-10-24 10:00:00 -0400
categories: probability statistics binomial-distribution
---

I've been on a bit of a "back to basics" kick lately, revisiting some of the foundational concepts in ML that I use every day but maybe haven't fully appreciated in a while. Linear regression is one of those things – it's literally the first algorithm most of us learn, but there's something elegant about understanding *exactly* why it works mathematically.

Today I want to walk through deriving the Normal Equation from scratch. Sure, every ML library just gives you the answer instantly, but there's real value in seeing how the calculus plays out. Plus, this derivation uses some really nice matrix calculus tricks that show up everywhere in ML.

## The Setup

The goal is simple: find the parameter vector $\boldsymbol{\theta}$ that minimizes the Sum of Squared Errors (SSE) between our predictions and the actual values. For a single data point $\mathbf{x}_n$, our linear model predicts:

$$ \hat{y}_n = \boldsymbol{\theta}^T \mathbf{x}_n $$

---

## Step 1: The Cost Function

The cost function $J(\boldsymbol{\theta})$ is just the sum of squared errors across all $N$ training points:

$$ J(\boldsymbol{\theta}) = \sum_{n=1}^{N} (y_n - \hat{y}_n)^2 = \sum_{n=1}^{N} (y_n - \boldsymbol{\theta}^T \mathbf{x}_n)^2 $$

We square the errors so positive and negative deviations don't cancel out, and to give extra penalty to large errors. Pretty standard stuff.

## Step 2: Moving to Matrix Notation

Working with summations gets tedious fast. Let me rewrite this using matrices, which makes the calculus much cleaner. Define:

- $\mathbf{y}$: vector of all target values $[y_1, y_2, \dots, y_N]^T$
- $\mathbf{X}$: the design matrix where each row is $\mathbf{x}_n^T$
- $\boldsymbol{\theta}$: our parameter vector

Now the predictions are just $\mathbf{X}\boldsymbol{\theta}$, and the cost function becomes:

$$ J(\boldsymbol{\theta}) = \| \mathbf{y} - \mathbf{X}\boldsymbol{\theta} \|_2^2 = (\mathbf{y} - \mathbf{X}\boldsymbol{\theta})^T (\mathbf{y} - \mathbf{X}\boldsymbol{\theta}) $$

Much cleaner!

---

## Step 3: Taking the Gradient

To minimize $J(\boldsymbol{\theta})$, I need to find where its gradient equals zero. First, let me expand the cost function:

$$ J(\boldsymbol{\theta}) = (\mathbf{y}^T - \boldsymbol{\theta}^T\mathbf{X}^T) (\mathbf{y} - \mathbf{X}\boldsymbol{\theta}) $$

$$ = \mathbf{y}^T\mathbf{y} - \mathbf{y}^T\mathbf{X}\boldsymbol{\theta} - \boldsymbol{\theta}^T\mathbf{X}^T\mathbf{y} + \boldsymbol{\theta}^T\mathbf{X}^T\mathbf{X}\boldsymbol{\theta} $$

Here's a neat trick: $\boldsymbol{\theta}^T\mathbf{X}^T\mathbf{y}$ is a scalar, so it equals its transpose $\mathbf{y}^T\mathbf{X}\boldsymbol{\theta}$. This means I can combine those middle terms:

$$ J(\boldsymbol{\theta}) = \mathbf{y}^T\mathbf{y} - 2\boldsymbol{\theta}^T\mathbf{X}^T\mathbf{y} + \boldsymbol{\theta}^T\mathbf{X}^T\mathbf{X}\boldsymbol{\theta} $$

Now taking the gradient with respect to $\boldsymbol{\theta}$ using standard matrix calculus:

$$ \nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta}) = \mathbf{0} - 2\mathbf{X}^T\mathbf{y} + 2\mathbf{X}^T\mathbf{X}\boldsymbol{\theta} $$

## Step 4: The Normal Equation

Setting the gradient to zero and solving for $\hat{\boldsymbol{\theta}}$:

$$ -2\mathbf{X}^T\mathbf{y} + 2\mathbf{X}^T\mathbf{X}\hat{\boldsymbol{\theta}} = \mathbf{0} $$

$$ \boxed{\mathbf{X}^T\mathbf{X}\hat{\boldsymbol{\theta}} = \mathbf{X}^T\mathbf{y}} $$

This is the famous Normal Equation! If $\mathbf{X}^T\mathbf{X}$ is invertible, we can solve directly for $\hat{\boldsymbol{\theta}} = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y}$.

### Connecting Back to Summations

Sometimes it's useful to see this in summation form to understand how individual data points contribute. The matrix form is actually equivalent to:

$$ \left(\sum_{n=1}^{N} \mathbf{x}_n \mathbf{x}_n^T\right) \hat{\boldsymbol{\theta}} = \sum_{n=1}^{N} y_n \mathbf{x}_n $$

The left side sums the outer products of each feature vector, while the right side sums each feature vector weighted by its target. Same equation, just different notation!

---

## What's Coming Next

This regression derivation got me thinking about probability distributions more broadly. I've been meaning to dive deeper into some distributions that show up constantly in Bayesian methods and probabilistic ML.

In my next couple of posts, I'm planning to work through the moments of the **Beta distribution** and the **Dirichlet distribution**. The Beta distribution is fascinating because it's the conjugate prior for binomial/Bernoulli distributions, and the Dirichlet is its multivariate generalization. Understanding their means, variances, and covariances from first principles will be really useful for when I work with these in practice.

Stay tuned! 📊
