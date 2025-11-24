---
layout: post
title: "Unbiased Estimators and the Uniform Distribution Constraint"
date: 2025-11-21
categories: [statistical-inference, estimation]
tags: [unbiased-estimators, uniform-distribution, impossibility-results]
math: true
---

Sometimes the math tells you that what you want simply can't exist. This exercise is one of those cases.

## The Problem

Let $x$ be a random variable with a uniform PDF on $[0, \frac{1}{\theta}]$ where $\theta > 0$. We want to find a function $g$ that defines an estimator $\hat{\theta} = g(x)$ of $\theta$ such that it's unbiased.

For an estimator to be unbiased, we need:

$$\mathbb{E}[\hat{\theta}] = \theta$$

In other words:

$$\int_0^{1/\theta} g(x) \cdot \theta \, dx = \theta$$

Since the PDF of the uniform distribution on $[0, \frac{1}{\theta}]$ is $p(x|\theta) = \theta$ for $x \in [0, \frac{1}{\theta}]$, this simplifies to:

$$\int_0^{1/\theta} g(x) \, dx = 1$$

## Why This Can't Work

The problem asks us to show that no such function $g$ exists. Here's the intuition: the upper limit of the integral depends on $\theta$, but the constraint requires the integral to equal 1 for *all* values of $\theta$. 

Let's think about what happens as $\theta$ changes. When $\theta$ increases, the interval $[0, \frac{1}{\theta}]$ shrinks. For the integral to stay constant at 1, $g(x)$ would need to somehow "know" about $\theta$ and adjust accordingly. But $g(x)$ is just a function of $x$ alone — it can't depend on $\theta$.

More formally, suppose such a $g$ existed. Then:

$$\int_0^{1/\theta} g(x) \, dx = 1 \quad \text{for all } \theta > 0$$

Differentiate both sides with respect to $\theta$:

$$\frac{d}{d\theta} \int_0^{1/\theta} g(x) \, dx = 0$$

By Leibniz's rule:

$$-\frac{1}{\theta^2} g\left(\frac{1}{\theta}\right) = 0$$

This means $g\left(\frac{1}{\theta}\right) = 0$ for all $\theta > 0$. But if $g$ is zero at every point in its domain (since $\frac{1}{\theta}$ covers the entire positive real line as $\theta$ varies), then the integral would be zero, not 1. Contradiction.

So no unbiased estimator exists in this setup. The uniform distribution's support depends on the parameter you're trying to estimate, and that dependency creates an impossible constraint.
