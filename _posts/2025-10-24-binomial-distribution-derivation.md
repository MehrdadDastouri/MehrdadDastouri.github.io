---
layout: post
title: "Breaking Down the Binomial Distribution: Mean and Variance"
date: 2025-10-24 11:00:00 -0400
categories: statistics probability
---

I was reviewing some old lecture notes the other day and realized I'd never actually sat down and derived the mean and variance of the Binomial distribution myself. Sure, I've *used* these formulas hundreds of times – $E[X] = np$ and $\text{Var}(X) = np(1-p)$ are practically muscle memory at this point – but understanding where they come from? That's different.

The Binomial shows up constantly: A/B testing, classification metrics, modeling binary outcomes. It's everywhere. So I figured it was worth working through the math from scratch.

## The Setup

A random variable $X \sim B(n, p)$ counts successes in $n$ independent trials, each with success probability $p$. The PMF is:

$$ P(X=k) = \binom{n}{k} p^k (1-p)^{n-k} $$

Nothing fancy – just counting how many ways we can get $k$ successes.

---

## Deriving the Mean

Start with the definition: $E[X] = \sum_{k=0}^{n} k \cdot P(X=k)$.

Plug in the PMF:

$$ E[X] = \sum_{k=0}^{n} k \cdot \frac{n!}{k!(n-k)!} p^k (1-p)^{n-k} $$

The $k=0$ term vanishes, so start at $k=1$. The $k$ cancels with one factor in $k!$:

$$ E[X] = \sum_{k=1}^{n} \frac{n!}{(k-1)!(n-k)!} p^k (1-p)^{n-k} $$

Here's where it gets neat – pull out $np$:

$$ E[X] = np \sum_{k=1}^{n} \frac{(n-1)!}{(k-1)!(n-k)!} p^{k-1} (1-p)^{n-k} $$

Substitute $m = n-1$ and $j = k-1$:

$$ E[X] = np \sum_{j=0}^{m} \binom{m}{j} p^{j} (1-p)^{m-j} $$

That's just a binomial distribution summing to 1. So:

$$ \boxed{E[X] = np} $$

Makes total sense. Run $n$ trials at probability $p$, expect $np$ successes.

---

## The Variance

For variance, I need $\text{Var}(X) = E[X^2] - (E[X])^2$. 

Instead of computing $E[X^2]$ directly (messy), there's a trick: find $E[X(X-1)]$ first.

$$ E[X(X-1)] = \sum_{k=0}^{n} k(k-1) \cdot \frac{n!}{k!(n-k)!} p^k (1-p)^{n-k} $$

Terms with $k=0$ and $k=1$ vanish. Start at $k=2$, and $k(k-1)$ cancels two factors of $k!$:

$$ E[X(X-1)] = \sum_{k=2}^{n} \frac{n!}{(k-2)!(n-k)!} p^k (1-p)^{n-k} $$

Pull out $n(n-1)p^2$:

$$ E[X(X-1)] = n(n-1)p^2 \sum_{k=2}^{n} \frac{(n-2)!}{(k-2)!(n-k)!} p^{k-2} (1-p)^{n-k} $$

Same deal – that sum equals 1:

$$ E[X(X-1)] = n(n-1)p^2 $$

Now use $E[X^2] = E[X(X-1)] + E[X]$:

$$ E[X^2] = n(n-1)p^2 + np $$

Variance:

$$ \text{Var}(X) = (n(n-1)p^2 + np) - (np)^2 $$

Expand:

$$ = n^2p^2 - np^2 + np - n^2p^2 = np(1-p) $$

$$ \boxed{\text{Var}(X) = np(1-p)} $$

---

## Why This Matters

The variance formula $np(1-p)$ has an interesting shape. When $p = 0.5$ (maximum uncertainty), variance peaks at $0.25n$. When $p$ approaches 0 or 1, variance drops – outcomes become predictable.

I run into this constantly in ML work. Logistic regression? It's modeling Bernoulli trials. Calibration metrics? Binomial distribution underneath. Even gradient updates in neural nets sometimes have binomial-like behavior when you're doing dropout.

Understanding these fundamentals makes debugging models way easier. When something looks off in your loss curves or confidence intervals, it often comes back to variance properties like this.


