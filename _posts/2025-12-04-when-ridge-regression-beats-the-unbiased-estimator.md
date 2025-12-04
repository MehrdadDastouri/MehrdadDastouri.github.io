---
layout: post
title: "When Ridge Regression Beats the Unbiased Estimator"
date: 2025-12-04
categories: [statistical-inference, regularization]
tags: [ridge-regression, bias-variance-tradeoff, mse, regularization]
math: true
---

Here's something that bothered me for weeks when I first learned ridge regression: we deliberately add bias to our estimator, and somehow that makes it better. The whole point of maximum likelihood is finding unbiased estimators that saturate the Cramér-Rao bound, right? So why would we intentionally mess that up?

The answer lives in the MSE decomposition. For any estimator, the mean squared error splits into two parts:

$$\text{MSE}(\hat{\theta}) = \text{variance}(\hat{\theta}) + \text{bias}^2(\hat{\theta}).$$

The MVU estimator has zero bias, so its MSE is just its variance. Ridge regression introduces a small bias but can reduce the variance dramatically, and if the variance drop is big enough, the total MSE goes down.

Consider a linear regression setup with one real-valued parameter $\theta_o$. Let $\hat{\theta}_{\text{MVU}}$ be the minimum variance unbiased estimator, and let $\hat{\theta}_b(\lambda)$ be the ridge estimator with regularization strength $\lambda$. The question is: when does

$$\text{MSE}\big(\hat{\theta}_b(\lambda)\big) < \text{MSE}\big(\hat{\theta}_{\text{MVU}}\big)?$$

The analysis shows this happens in two regimes. If the true parameter is small relative to the noise—specifically, if

$$\theta_o^2 \le \frac{\sigma_\eta^2}{N},$$

then ridge wins for any positive $\lambda$. The signal is weak enough that the variance reduction dominates, no matter how much bias you add.

In the opposite case, when $\theta_o^2 > \sigma_\eta^2 / N$, ridge still wins but only for a restricted range of $\lambda$. You need

$$\lambda \in \left(0, \frac{2\sigma_\eta^2}{\theta_o^2 - \sigma_\eta^2/N}\right).$$

Too much regularization overdoes the bias, and the MSE climbs back above the unbiased baseline. The optimal choice sits right in the middle at

$$\lambda_* = \frac{\sigma_\eta^2}{\theta_o^2}.$$

This is the ratio of noise variance to signal strength squared. When the signal is strong, you barely regularize. When the noise dominates, you shrink aggressively.

What strikes me about this result is how sharp the threshold is. The criterion $\theta_o^2 \le \sigma_\eta^2 / N$ draws a clean line between the regime where any regularization helps and the regime where you need to tune carefully. It's not a fuzzy trade-off—it's a precise boundary that depends only on the signal-to-noise ratio and the sample size.

In practice, you never know $\theta_o$ in advance, so you can't compute $\lambda_*$ directly. But cross-validation approximates this tuning by estimating how much bias the data can tolerate before the variance savings disappear. The math here explains why that search works and why ridge regression dominates least squares in high-dimensional settings where many parameters are small.
