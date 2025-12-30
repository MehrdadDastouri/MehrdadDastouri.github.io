---
layout: post
title: "Uniqueness of Solutions in Linear Systems"
date: 2025-12-30
categories: [linear-algebra]
tags: [positive-definite, singular-matrix, linear-systems]
math: true
---

The system $\Sigma \theta = p$ where $\Sigma$ is a covariance matrix (so symmetric and positive semi-definite at least). Two cases depending on whether $\Sigma$ is strictly positive definite or singular.

If $\Sigma > 0$ meaning positive definite, then all eigenvalues are strictly positive, which means $\Sigma$ is invertible. The unique solution is just $\theta = \Sigma^{-1} p$. Nothing more to say.

When $\Sigma$ is singular things get interesting. Singular means at least one eigenvalue is zero, so there exists a non-zero vector $v$ in the null space with $\Sigma v = 0$. Now if $\theta^*$ is any solution to $\Sigma \theta = p$, then $\theta^* + \alpha v$ is also a solution for any scalar $\alpha$ because $\Sigma(\theta^* + \alpha v) = \Sigma \theta^* + \alpha \Sigma v = p + 0 = p$. Since $\alpha$ can be anything, that's infinitely many solutions.

One subtlety. For solutions to exist at all when $\Sigma$ is singular, $p$ must lie in the column space of $\Sigma$. If $p$ has any component in the null space of $\Sigma^T$ (which equals the null space of $\Sigma$ since $\Sigma$ is symmetric) then there's no solution. But assuming a solution exists, it's never unique when $\Sigma$ is singular.
