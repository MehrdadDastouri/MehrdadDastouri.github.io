---
layout: post
title: "Least Squares for Linear Regression"
date: 2025-11-19
categories: [linear-regression, optimization]
tags: [least-squares, normal-equations, linear-algebra]
math: true
---

The normal equations for least squares — you've probably seen them a hundred times. But let's actually *prove* why they work.

## Setup

We have data points $(x_n, y_n)$ for $n = 1, \ldots, N$, and we want to fit a linear model:

$$y_n = x_n^T \hat{\theta}$$

The goal is to minimize the sum of squared errors:

$$\mathcal{L}(\theta) = \sum_{n=1}^N (y_n - x_n^T \theta)^2$$

In matrix form, stack everything:

$$\mathbf{y} = \begin{bmatrix} y_1 \\ \vdots \\ y_N \end{bmatrix}, \quad \mathbf{X} = \begin{bmatrix} x_1^T \\ \vdots \\ x_N^T \end{bmatrix}$$

Then the loss becomes:

$$\mathcal{L}(\theta) = \|\mathbf{y} - \mathbf{X}\theta\|^2$$

## Taking the Derivative

Expand the squared norm:

$$\mathcal{L}(\theta) = (\mathbf{y} - \mathbf{X}\theta)^T (\mathbf{y} - \mathbf{X}\theta)$$

$$= \mathbf{y}^T \mathbf{y} - 2 \mathbf{y}^T \mathbf{X} \theta + \theta^T \mathbf{X}^T \mathbf{X} \theta$$

Now differentiate with respect to $\theta$ and set to zero:

$$\nabla_\theta \mathcal{L} = -2 \mathbf{X}^T \mathbf{y} + 2 \mathbf{X}^T \mathbf{X} \theta = 0$$

Rearranging gives the **normal equations**:

$$\mathbf{X}^T \mathbf{X} \hat{\theta} = \mathbf{X}^T \mathbf{y}$$

If $\mathbf{X}^T \mathbf{X}$ is invertible (i.e., columns of $\mathbf{X}$ are linearly independent), then:

$$\hat{\theta} = (\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T \mathbf{y}$$

This is exactly Eq. (3.13) from the book.

## Why It Matters

This isn't just some abstract formula. The normal equations are the foundation of:

- Linear regression (obviously)
- Ridge regression (add $\lambda I$ to $\mathbf{X}^T \mathbf{X}$)
- Kalman filtering (same structure, recursive form)
- Neural network weight updates in the linear case

What I find neat is that $(\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T$ is the **pseudoinverse** of $\mathbf{X}$ when $\mathbf{X}$ isn't square. So least squares is really just projection onto the column space of $\mathbf{X}$.
