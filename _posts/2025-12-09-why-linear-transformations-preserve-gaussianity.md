---
layout: post
title: "Why Linear Transformations Preserve Gaussianity"
date: 2025-12-09
categories: [statistical-inference, probability-theory]
tags: [gaussian, linear-transformation, characteristic-function, covariance]
math: true
---

There's a fact about Gaussian random variables that gets used constantly in statistics and signal processing, often without much comment: if you take a bunch of jointly Gaussian variables and form any linear combination of them, the result is still Gaussian. It sounds almost obvious once you've heard it enough times, but the first time I tried to prove it rigorously, I realized I didn't actually know why it was true.

The setup is this. Suppose we have $l$ jointly Gaussian random variables $\{x_1, x_2, \ldots, x_l\}$, which we can stack into a vector $\mathbf{x} := [x_1, x_2, \ldots, x_l]^T$. Now take any nonsingular matrix $A \in \mathbb{R}^{l \times l}$ and form a new vector $\mathbf{y} = A\mathbf{x}$. The claim is that the components of $\mathbf{y}$ are also jointly Gaussian.

The cleanest way to see this is through characteristic functions. Recall that the characteristic function of a random vector $\mathbf{x}$ is defined as

$$\phi_{\mathbf{x}}(\mathbf{t}) := \mathbb{E}\left[e^{i\mathbf{t}^T\mathbf{x}}\right].$$

For a Gaussian vector with mean $\boldsymbol{\mu}$ and covariance matrix $\Sigma$, this takes the form

$$\phi_{\mathbf{x}}(\mathbf{t}) = \exp\left(i\mathbf{t}^T\boldsymbol{\mu} - \frac{1}{2}\mathbf{t}^T\Sigma\mathbf{t}\right).$$

Now let's compute the characteristic function of $\mathbf{y} = A\mathbf{x}$. For any vector $\mathbf{s}$,

$$\phi_{\mathbf{y}}(\mathbf{s}) = \mathbb{E}\left[e^{i\mathbf{s}^T\mathbf{y}}\right] = \mathbb{E}\left[e^{i\mathbf{s}^TA\mathbf{x}}\right] = \mathbb{E}\left[e^{i(A^T\mathbf{s})^T\mathbf{x}}\right].$$

This is just the characteristic function of $\mathbf{x}$ evaluated at the vector $\mathbf{t} = A^T\mathbf{s}$:

$$\phi_{\mathbf{y}}(\mathbf{s}) = \phi_{\mathbf{x}}(A^T\mathbf{s}) = \exp\left(i(A^T\mathbf{s})^T\boldsymbol{\mu} - \frac{1}{2}(A^T\mathbf{s})^T\Sigma(A^T\mathbf{s})\right).$$

Simplifying the exponent:

$$\phi_{\mathbf{y}}(\mathbf{s}) = \exp\left(i\mathbf{s}^TA\boldsymbol{\mu} - \frac{1}{2}\mathbf{s}^TA\Sigma A^T\mathbf{s}\right).$$

This is exactly the characteristic function of a Gaussian vector with mean $A\boldsymbol{\mu}$ and covariance $A\Sigma A^T$. Since characteristic functions uniquely determine distributions, we're done: $\mathbf{y}$ is jointly Gaussian.

What I find satisfying about this proof is how the structure of the Gaussian characteristic function—a quadratic form in the exponent—is preserved under linear transformation. The linearity of $A$ interacts perfectly with the quadratic nature of the Gaussian, and everything stays in the same family.

There's an alternative approach using the density directly. If $A$ is nonsingular, we can use the change of variables formula. The density of $\mathbf{y}$ is

$$p_{\mathbf{y}}(\mathbf{y}) = p_{\mathbf{x}}(A^{-1}\mathbf{y}) \cdot |\det(A^{-1})| = p_{\mathbf{x}}(A^{-1}\mathbf{y}) \cdot \frac{1}{|\det(A)|}.$$

Substituting the Gaussian density for $\mathbf{x}$ and simplifying, you again get a Gaussian density for $\mathbf{y}$. But this approach requires $A$ to be invertible. The characteristic function argument is more general—it works even when $A$ is rectangular, which is useful when you want to project a high-dimensional Gaussian down to a lower-dimensional space.

A direct consequence of this result is that any linear combination of jointly Gaussian variables is also Gaussian. If you want a single scalar $z = \mathbf{a}^T\mathbf{x}$ for some vector $\mathbf{a}$, this is just a special case where $A = \mathbf{a}^T$ is a $1 \times l$ matrix. The result $z$ is Gaussian with mean $\mathbf{a}^T\boldsymbol{\mu}$ and variance $\mathbf{a}^T\Sigma\mathbf{a}$.

This property is why Gaussians are so central to linear models. In regression, we model observations as linear combinations of parameters plus noise. If everything is Gaussian, then all the derived quantities—fitted values, residuals, test statistics—remain Gaussian, and we can compute their distributions exactly. Without closure under linear transformations, the whole edifice of classical linear inference would fall apart.
