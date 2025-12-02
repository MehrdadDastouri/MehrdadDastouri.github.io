---
layout: post
title: "Equivalence of Centered and Uncentered Regularization in Linear Models"
date: 2025-12-03
categories: [statistical-inference, regularization]
tags: [ridge-regression, centered-regularization, bias-term, least-squares]
math: true
---

In linear regression with a bias term, the model has the form

$$y_n = \theta_0 + \sum_{i=1}^l \theta_i x_{ni}, \quad n=1,2,\ldots,N.$$

When regularization is applied, the typical approach penalizes the squared norm of the weight vector excluding the bias. The objective becomes

$$L(\boldsymbol{\theta}, \lambda)
= \sum_{n=1}^N \left(y_n - \theta_0 - \sum_{i=1}^l \theta_i x_{ni}\right)^2
+ \lambda \sum_{i=1}^l \theta_i^2.$$

This formulation treats the bias separately because penalizing it would shift the optimal solution away from the data's natural center. The bias absorbs the mean of the target, and forcing it toward zero distorts the fit unnecessarily.

An alternative perspective emerges by centering the data first. Define the sample means

$$\bar{y} := \frac{1}{N}\sum_{n=1}^N y_n, \quad
\bar{x}_i := \frac{1}{N}\sum_{n=1}^N x_{ni}.$$

The centered variables are

$$\tilde{y}_n := y_n - \bar{y}, \quad
\tilde{x}_{ni} := x_{ni} - \bar{x}_i.$$

Rewriting the loss in terms of centered quantities gives

$$L(\boldsymbol{\theta}, \lambda)
= \sum_{n=1}^N \left(\tilde{y}_n - \sum_{i=1}^l \theta_i \tilde{x}_{ni}\right)^2
+ \lambda \sum_{i=1}^l \theta_i^2.$$

This centered formulation has no explicit bias term because the centering operation removes the mean structure from both the inputs and the targets. The regularization penalty applies only to the slope parameters, exactly as before.

The two formulations are equivalent in the sense that they produce the same optimal weights $\theta_1, \ldots, \theta_l$. Once these weights are found, the bias in the uncentered version is recovered by

$$\hat{\theta}_0 = \bar{y} - \sum_{i=1}^l \hat{\theta}_i \bar{x}_i.$$

This relationship shows that the bias simply adjusts for the displacement between the centered coordinate system and the original one. The slope coefficients remain unchanged because the regularization structure respects the geometry of the problem.

From a computational standpoint, solving the centered problem is often cleaner. The design matrix has zero column means, which can improve numerical stability and makes the role of regularization more transparent. The uncentered formulation is more direct for interpretation, but both paths lead to the same statistical object.
