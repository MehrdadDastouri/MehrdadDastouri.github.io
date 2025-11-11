---
layout: post
title: "Autocorrelation in Wide-Sense Stationary Processes"
date: 2025-11-11
categories: [signal-processing, stochastic-processes]
tags: [wss, autocorrelation, stationary-processes]
math: true
---

Wide-sense stationary (WSS) processes are everywhere in signal processing. The key property is that their first two moments don't change over time—constant mean and autocorrelation that only depends on the time lag.

## Basic WSS Properties

For a WSS process $r(t)$ with autocorrelation $r_r(k)$:

$$
r(0) \geq |r(k)|, \quad \forall k \in \mathbb{Z}
$$

This just says the maximum correlation is at zero lag. Makes sense—a signal correlates with itself perfectly at the same time, and that correlation can only decrease (in magnitude) as you shift in time.

## Joint WSS Processes

When you have two jointly WSS processes $r(t)$ and $v(t)$, their cross-correlation $r_{uv}(k)$ satisfies:

$$
r_u(0) \cdot r_v(0) \geq |r_{uv}(k)|^2, \quad \forall k \in \mathbb{Z}
$$

This is basically Cauchy-Schwarz at work. The cross-correlation at any lag is bounded by the geometric mean of the autocorrelations at zero lag.

## Why This Matters

These bounds are really useful when you're analyzing the output of a system. If you know your input is WSS and you know the impulse response, you can characterize how correlations propagate through the system.

For example, if you're filtering a signal, you know the output autocorrelation can't exceed the input autocorrelation at zero lag, scaled by the filter's energy. So even without computing everything explicitly, you get bounds on what's possible.

What's interesting is how these simple inequalities capture fundamental limits on how much structure you can have in a random process. You can't have arbitrarily strong correlations at all lags without violating stationarity.
