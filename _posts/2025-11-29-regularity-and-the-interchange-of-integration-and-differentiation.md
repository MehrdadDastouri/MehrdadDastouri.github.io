---
layout: post
title: "Regularity and the Interchange of Integration and Differentiation"
date: 2025-11-29
categories: [statistical-inference, estimation]
tags: [cramer-rao, regularity-conditions, differentiation-under-integral]
math: true
---

The regularity condition is essentially the permission slip that lets you move derivatives across integrals without breaking anything. When the PDF behaves smoothly enough with respect to the parameter, differentiating the likelihood becomes a clean operation rather than an act of faith.

Starting from the basic identity, the PDF must integrate to one for all parameter values. This means

$$\frac{d}{d\theta} \int p(\mathcal{D}|\theta)d\mathcal{D} = \frac{d}{d\theta} 1 = 0.$$

If differentiation under the integral is legal, then

$$\int \frac{\partial}{\partial\theta} p(\mathcal{D}|\theta)d\mathcal{D} = 0.$$

Using the log‑likelihood simplifies the structure. With $p>0$ and sufficiently smooth,

$$\frac{\partial}{\partial\theta}\log p = \frac{1}{p}\frac{\partial p}{\partial\theta}.$$

Integrating both sides multiplied by the PDF gives

$$\int p \frac{\partial}{\partial\theta}\log p \, d\mathcal{D}
= \int \frac{\partial p}{\partial\theta} d\mathcal{D} = 0.$$

This means the expected score is zero:

$$\mathbb{E}\left[\frac{\partial}{\partial\theta}\log p(\mathcal{D}|\theta)\right] = 0.$$

Once this anchor is in place, the Fisher information arrives in its usual canonical form

$$I(\theta)
= -\mathbb{E}\left[\frac{\partial^2}{\partial\theta^2}\log p(\mathcal{D}|\theta)\right],$$

and all downstream CRLB derivations rely on exactly this interchangeability. Everything collapses if the regularity condition fails; with it, the information geometry behaves the way it should.
