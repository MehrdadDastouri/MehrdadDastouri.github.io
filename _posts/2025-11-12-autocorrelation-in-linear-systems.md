---
layout: post
title: "Autocorrelation in Linear Systems"
date: 2025-11-12
categories: [signal-processing, linear-systems]
tags: [autocorrelation, impulse-response, wss, convolution]
math: true
---

When you pass a WSS process through a linear time-invariant (LTI) system, there's a clean relationship between the input and output autocorrelations. It all comes down to convolution.

## The Setup

Say we have an input WSS process $u(n)$ with autocorrelation $r_u(k)$, and we feed it through a system with impulse response $w_n$. The output is:

$$
d(n) = \sum_{m=-\infty}^{\infty} w_m \, u(n-m)
$$

The question is: how does $r_d(k)$, the output autocorrelation, relate to $r_u(k)$?

## Deriving the Relationship

Start with the definition of autocorrelation:

$$
r_d(k) = \mathbb{E}[d(n) d(n-k)]
$$

Substituting the convolution:

$$
= \mathbb{E}\left[\sum_{m} w_m u(n-m) \sum_{\ell} w_\ell u(n-k-\ell)\right]
$$

Since expectation is linear, we can pull it inside:

$$
= \sum_{m} \sum_{\ell} w_m w_\ell \, \mathbb{E}[u(n-m) u(n-k-\ell)]
$$

The inner expectation is just $r_u(k + \ell - m)$ by the WSS property. So:

$$
r_d(k) = \sum_{m} \sum_{\ell} w_m w_\ell \, r_u(k + \ell - m)
$$

Now here's the trick: define $j = \ell - m$, which gives:

$$
r_d(k) = \sum_{m} w_m \sum_{j} w_{m+j} \, r_u(k - j)
$$

The inner sum is the convolution of $w$ with its time-reversed version, evaluated at $k-j$. In other words:

$$
r_d(k) = r_u(k) * w_k * w_{-k}
$$

That's the result: the output autocorrelation is the input autocorrelation convolved with the impulse response and its time-reversal.

## What This Tells Us

This formula is surprisingly useful. It says that:
- The system's impulse response acts like a "smoothing filter" on the input autocorrelation structure
- If your system has a short impulse response, correlations in the output decay faster
- If the impulse response is symmetric, things simplify even more

For example, a simple moving average filter with $w_n = 1/M$ for $n = 0, \ldots, M-1$ will spread out the input correlation over $M$ lags. The output becomes "smoother" in time.

What I find neat is how this connects time-domain filtering with correlation structure. You're not just filtering the signal values—you're filtering the *correlation pattern* itself. And that convolution with $w_{-k}$ captures exactly how the system's memory affects correlations at different lags.
