---
layout: post
title: "Cramér–Rao Bound for the Linear LS Model and Asymptotic Efficiency"
date: 2025-11-30
categories: [statistical-inference, estimation]
tags: [cramer-rao, least-squares, linear-model, asymptotic-efficiency]
math: true
---

In the simple linear model

$$y_n = \theta x_n + \eta_n,$$

the structure is clean enough that the Cramér–Rao bound can be written down essentially in closed form. The inputs $x_n$ are independent with zero mean and variance $\sigma_x^2$, while the noise is Gaussian with variance $\sigma_\eta^2$ and is independent of the inputs.

The conditional likelihood for a single observation is

$$p(y_n|\theta,x_n) = \frac{1}{\sqrt{2\pi\sigma_\eta^2}}
\exp\!\left(-\frac{(y_n - \theta x_n)^2}{2\sigma_\eta^2}\right).$$

Differentiating its log with respect to $\theta$ yields

$$\frac{\partial}{\partial\theta}\log p(y_n|\theta,x_n)
= \frac{x_n(y_n - \theta x_n)}{\sigma_\eta^2}
= \frac{x_n \eta_n}{\sigma_\eta^2}.$$

Since $x_n$ and $\eta_n$ are independent, the Fisher information per sample becomes

$$I_1(\theta)
= \mathbb{E}\left[\frac{x_n^2 \eta_n^2}{\sigma_\eta^4}\right]
= \frac{\sigma_x^2}{\sigma_\eta^2}.$$

With $N$ observations, the information adds linearly:

$$I_N(\theta) = N \frac{\sigma_x^2}{\sigma_\eta^2}.$$

Thus the Cramér–Rao lower bound is

$$\operatorname{var}(\hat{\theta}) \ge
\frac{\sigma_\eta^2}{N\sigma_x^2}.$$

The least‑squares estimator is

$$\hat{\theta}_{LS}
= \frac{\sum x_n y_n}{\sum x_n^2}
= \theta + \frac{\sum x_n\eta_n}{\sum x_n^2}.$$

Its bias vanishes because the noise has zero mean. The variance is

$$\operatorname{var}(\hat{\theta}_{LS})
= \sigma_\eta^2 \, \mathbb{E}\left[\frac{1}{\sum x_n^2}\right].$$

As $N$ grows, the denominator concentrates through the law of large numbers:

$$\frac{1}{N}\sum x_n^2 \to \sigma_x^2,$$

which implies

$$\operatorname{var}(\hat{\theta}_{LS})
\approx \frac{\sigma_\eta^2}{N\sigma_x^2}.$$

The LS estimator therefore meets the CRLB **asymptotically**, even though for finite $N$ it stays slightly above it. This is exactly the sense in which LS is called asymptotically efficient for this model.
