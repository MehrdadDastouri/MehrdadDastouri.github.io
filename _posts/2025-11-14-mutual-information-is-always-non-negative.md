---
layout: post
title: "Mutual Information is Always Non-Negative"
date: 2025-11-14
categories: [information-theory, probability]
tags: [mutual-information, kl-divergence, entropy]
math: true
---

Mutual information $I(X; Y)$ measures how much knowing one random variable tells you about another. A fundamental property is that it's always non-negative:

$$
I(X; Y) \geq 0
$$

with equality if and only if $X$ and $Y$ are independent.

## Using the Logarithm Bound

The standard definition is:

$$
I(X; Y) = \sum_x \sum_y p(x,y) \ln \frac{p(x,y)}{p(x)p(y)}
$$

This is just the KL divergence between the joint distribution $p(x,y)$ and the product of marginals $p(x)p(y)$.

From the previous result, we know that $\ln z \leq z - 1$ for all $z > 0$. So:

$$
\ln \frac{p(x,y)}{p(x)p(y)} \leq \frac{p(x,y)}{p(x)p(y)} - 1
$$

Multiply both sides by $p(x,y)$ and sum:

$$
I(X; Y) \leq \sum_x \sum_y p(x,y) \left(\frac{p(x,y)}{p(x)p(y)} - 1\right)
$$

The right side simplifies:

$$
= \sum_x \sum_y p(x,y) - \sum_x \sum_y p(x)p(y)
$$

Both sums equal 1, so:

$$
I(X; Y) \leq 1 - 1 = 0
$$

Wait, that gives us the wrong direction. Let me reconsider.

Actually, the issue is that I applied the bound directly. Instead, use the fact that for the KL divergence:

$$
D_{KL}(P \| Q) = \sum_x p(x) \ln \frac{p(x)}{q(x)}
$$

Apply $\ln z \leq z - 1$ with $z = p(x)/q(x)$:

$$
\ln \frac{p(x)}{q(x)} \leq \frac{p(x)}{q(x)} - 1
$$

Multiply by $p(x)$:

$$
p(x) \ln \frac{p(x)}{q(x)} \leq p(x) \left(\frac{p(x)}{q(x)} - 1\right) = p(x) - q(x)
$$

Sum over $x$:

$$
D_{KL}(P \| Q) \leq \sum_x (p(x) - q(x)) = 1 - 1 = 0
$$

But we know $D_{KL}(P \| Q) \geq 0$. So actually we get $D_{KL}(P \| Q) = 0$ only when $P = Q$.

Hmm, this derivation shows $D_{KL} \leq 0$, but we know it's non-negative. The resolution is that the inequality $\ln z \leq z - 1$ becomes equality only at $z = 1$, and the concavity of $\ln$ actually gives us:

$$
-\ln z \geq -z + 1 \implies \ln z \leq z - 1
$$

For KL divergence, using $-\ln(q(x)/p(x)) = \ln(p(x)/q(x))$:

$$
D_{KL}(P \| Q) = -\sum_x p(x) \ln \frac{q(x)}{p(x)} \geq -\sum_x p(x)\left(\frac{q(x)}{p(x)} - 1\right) = 0
$$

So $I(X; Y) \geq 0$ follows immediately since mutual information is just a KL divergence.

## What This Means

Mutual information being non-negative means you can never have *negative* information—learning about $Y$ can't make you know *less* about $X$. At worst, they're independent and you gain nothing.

The connection to that simple logarithm bound is neat. It's one of those cases where an elementary inequality from calculus turns into a fundamental constraint in information theory.
