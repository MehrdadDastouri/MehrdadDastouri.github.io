---
layout: post
title: "A Weighted Logarithm Inequality"
date: 2025-11-15
categories: [mathematics, information-theory]
tags: [inequalities, entropy, logarithms]
math: true
---

Here's an inequality that shows up when working with entropy and relative measures. If you have two sets of positive numbers $a_i$ and $b_i$ where the $a_i$ form a probability distribution and the $b_i$ sum to at most 1:

$$
\sum_{i=1}^{M} a_i = 1, \quad \sum_{i=1}^{M} b_i \leq 1
$$

then:

$$
-\sum_{i=1}^{M} a_i \ln a_i \leq -\sum_{i=1}^{M} a_i \ln b_i
$$

This basically says the entropy computed with weights $a_i$ is bounded above by the cross-entropy when you use $b_i$ instead.

## The Proof

Start with the logarithm inequality from earlier: $\ln x \leq x - 1$ for all $x > 0$.

Apply this to $x = b_i / a_i$:

$$
\ln \frac{b_i}{a_i} \leq \frac{b_i}{a_i} - 1
$$

Multiply both sides by $a_i$:

$$
a_i \ln b_i - a_i \ln a_i \leq b_i - a_i
$$

Rearrange:

$$
a_i \ln b_i \leq a_i \ln a_i + b_i - a_i
$$

Multiply through by $-1$ (flipping the inequality):

$$
-a_i \ln b_i \geq -a_i \ln a_i - b_i + a_i
$$

Now sum over all $i$:

$$
-\sum_{i=1}^{M} a_i \ln b_i \geq -\sum_{i=1}^{M} a_i \ln a_i - \sum_{i=1}^{M} b_i + \sum_{i=1}^{M} a_i
$$

The last two sums give:

$$
\sum_{i=1}^{M} a_i = 1, \quad \sum_{i=1}^{M} b_i \leq 1
$$

So:

$$
-\sum_{i=1}^{M} a_i \ln b_i \geq -\sum_{i=1}^{M} a_i \ln a_i - \sum_{i=1}^{M} b_i + 1 \geq -\sum_{i=1}^{M} a_i \ln a_i
$$

Rearranging gives the desired result.

## What This Tells Us

This inequality captures why entropy is maximized when uncertainty is highest. The term $-\sum a_i \ln a_i$ is the entropy of the distribution $\{a_i\}$. The term $-\sum a_i \ln b_i$ is the cross-entropy between $\{a_i\}$ and $\{b_i\}$.

What's neat is that this works even when $\{b_i\}$ doesn't sum to exactly 1—as long as it sums to *at most* 1, the inequality holds. That extra slack in the constraint shows up in the proof when we bound $1 - \sum b_i \geq 0$.

This is one of those result that feels very information-theoretic but has purely algebraic roots in that simple logarithm bound.
