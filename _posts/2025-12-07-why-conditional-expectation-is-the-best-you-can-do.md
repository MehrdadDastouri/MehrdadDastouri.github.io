---
layout: post
title: "Why Conditional Expectation Is the Best You Can Do"
date: 2025-12-07
categories: [statistical-inference, estimation]
tags: [mse, conditional-expectation, optimal-prediction, regression]
math: true
---

I was working through a prediction problem last week and kept second-guessing myself. I had two random vectors, $\mathbf{y}$ in $\mathbb{R}^k$ and $\mathbf{x}$ in $\mathbb{R}^l$, jointly distributed, and I needed to estimate $\mathbf{y}$ given an observation $\mathbf{x} = \boldsymbol{x}$. My first instinct was to try something clever—maybe a weighted combination, maybe some nonlinear transformation that exploits the structure of the problem. But every time I ran the numbers, the conditional expectation $\mathbb{E}[\mathbf{y} \mid \mathbf{x}]$ came out on top. Eventually I sat down and proved it to myself, and the argument is cleaner than I expected.

The claim is this: among all possible estimators $\hat{\mathbf{y}} = g(\mathbf{x})$ that are functions of $\mathbf{x}$, the one that minimizes the mean squared error is exactly the conditional expectation. No other function of $\mathbf{x}$ can do better.

Let $g(\mathbf{x})$ be any estimator. The MSE is

$$\text{MSE}(g) = \mathbb{E}\left[\|\mathbf{y} - g(\mathbf{x})\|^2\right].$$

The trick is to add and subtract $\mathbb{E}[\mathbf{y} \mid \mathbf{x}]$ inside the norm. Write

$$\mathbf{y} - g(\mathbf{x}) = \big(\mathbf{y} - \mathbb{E}[\mathbf{y} \mid \mathbf{x}]\big) + \big(\mathbb{E}[\mathbf{y} \mid \mathbf{x}] - g(\mathbf{x})\big).$$

Expanding the squared norm gives three terms:

$$\|\mathbf{y} - g(\mathbf{x})\|^2 = \|\mathbf{y} - \mathbb{E}[\mathbf{y} \mid \mathbf{x}]\|^2 + \|\mathbb{E}[\mathbf{y} \mid \mathbf{x}] - g(\mathbf{x})\|^2 + 2\big(\mathbf{y} - \mathbb{E}[\mathbf{y} \mid \mathbf{x}]\big)^T\big(\mathbb{E}[\mathbf{y} \mid \mathbf{x}] - g(\mathbf{x})\big).$$

Now take expectations. The cross term vanishes, and this is where the magic happens. Condition on $\mathbf{x}$ first:

$$\mathbb{E}\left[\big(\mathbf{y} - \mathbb{E}[\mathbf{y} \mid \mathbf{x}]\big)^T\big(\mathbb{E}[\mathbf{y} \mid \mathbf{x}] - g(\mathbf{x})\big) \,\Big|\, \mathbf{x}\right].$$

Given $\mathbf{x}$, the term $\mathbb{E}[\mathbf{y} \mid \mathbf{x}] - g(\mathbf{x})$ is just a constant vector. Pull it out:

$$\big(\mathbb{E}[\mathbf{y} \mid \mathbf{x}] - g(\mathbf{x})\big)^T \mathbb{E}\left[\mathbf{y} - \mathbb{E}[\mathbf{y} \mid \mathbf{x}] \,\Big|\, \mathbf{x}\right].$$

But $\mathbb{E}[\mathbf{y} - \mathbb{E}[\mathbf{y} \mid \mathbf{x}] \mid \mathbf{x}] = \mathbb{E}[\mathbf{y} \mid \mathbf{x}] - \mathbb{E}[\mathbf{y} \mid \mathbf{x}] = \mathbf{0}$. The whole cross term is zero.

What remains is

$$\text{MSE}(g) = \mathbb{E}\left[\|\mathbf{y} - \mathbb{E}[\mathbf{y} \mid \mathbf{x}]\|^2\right] + \mathbb{E}\left[\|\mathbb{E}[\mathbf{y} \mid \mathbf{x}] - g(\mathbf{x})\|^2\right].$$

The first term doesn't depend on $g$ at all—it's the irreducible error, the variance of $\mathbf{y}$ around its conditional mean. The second term is always non-negative and equals zero only when $g(\mathbf{x}) = \mathbb{E}[\mathbf{y} \mid \mathbf{x}]$ almost surely.

So the conditional expectation achieves the minimum MSE, and any other estimator adds extra error on top of the irreducible part.

What I find striking about this result is how general it is. There's no assumption about Gaussianity, no linearity requirement, no constraint on the form of $g$. You're searching over all measurable functions of $\mathbf{x}$, and the winner is always $\mathbb{E}[\mathbf{y} \mid \mathbf{x}]$. The proof doesn't even care about the dimension of the spaces involved.

This also explains why linear regression works the way it does. When $(\mathbf{y}, \mathbf{x})$ are jointly Gaussian, the conditional expectation happens to be linear in $\mathbf{x}$, so restricting to linear estimators costs you nothing. But in the general case, linear regression is only optimal within the class of linear functions—it's an approximation to the true conditional expectation, not a replacement for it.

One practical consequence: if you're building a predictor and you have enough data to estimate $\mathbb{E}[\mathbf{y} \mid \mathbf{x}]$ nonparametrically, you should. Any parametric assumption you impose is a bet that the true conditional expectation lies in your model class. Sometimes that bet pays off through lower variance, but the target you're approximating is always the same.
