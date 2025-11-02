---
layout: post
title: "Breaking Down the Binomial Distribution: Mean and Variance"
date: 2025-10-24 11:00:00 -0400
categories: statistics probability
---

The Binomial distribution is one of those foundational concepts that keeps showing up everywhere in data science and machine learning. Whether you're doing A/B testing, modeling binary outcomes, or working with classification problems, understanding how it behaves is essential.

I've been revisiting some probability fundamentals lately, and I wanted to work through the derivations of the Binomial distribution's mean and variance from scratch. Sure, I could just look up the formulas, but there's something satisfying about seeing *why* they work the way they do.

## Quick Setup

A random variable $X$ follows a binomial distribution $X \sim B(n, p)$ when we're counting successes in $n$ independent trials, each with success probability $p$. The probability mass function is:

$$ P(X=k) = \binom{n}{k} p^k (1-p)^{n-k} $$

where $k$ is the number of successes we observe.

---

## Finding the Mean

The expected value is defined as $E[X] = \sum_{k=0}^{n} k \cdot P(X=k)$. Let's plug in our PMF:

$$ E[X] = \sum_{k=0}^{n} k \cdot \frac{n!}{k!(n-k)!} p^k (1-p)^{n-k} $$

The first term (when $k=0$) contributes nothing, so I'll start from $k=1$. Also, the $k$ in front cancels with one factor in $k!$:

$$ E[X] = \sum_{k=1}^{n} \frac{n!}{(k-1)!(n-k)!} p^k (1-p)^{n-k} $$

Now here's a neat trick – I can factor out $n$ and $p$:

$$ E[X] = np \sum_{k=1}^{n} \frac{(n-1)!}{(k-1)!(n-k)!} p^{k-1} (1-p)^{n-k} $$

If I substitute $m = n-1$ and $j = k-1$, this becomes:

$$ E[X] = np \sum_{j=0}^{m} \frac{m!}{j!(m-j)!} p^{j} (1-p)^{m-j} $$

Wait – that sum looks familiar! It's just the total probability for a binomial distribution $B(m, p)$, which must equal 1. So:

$$ \boxed{E[X] = np} $$

Pretty intuitive, right? If you run $n$ trials with probability $p$ each, you expect $np$ successes on average.

---

## Working Out the Variance

For variance, I need $\text{Var}(X) = E[X^2] - (E[X])^2$. I already have $E[X]$, so let me find $E[X^2]$.

There's a clever approach here: instead of computing $E[X^2]$ directly, I'll first find $E[X(X-1)]$, which has a nicer form:

$$ E[X(X-1)] = \sum_{k=0}^{n} k(k-1) \cdot \frac{n!}{k!(n-k)!} p^k (1-p)^{n-k} $$

Both $k=0$ and $k=1$ give zero, so start at $k=2$. The $k(k-1)$ term cancels with the first two factors of $k!$:

$$ E[X(X-1)] = \sum_{k=2}^{n} \frac{n!}{(k-2)!(n-k)!} p^k (1-p)^{n-k} $$

Factoring out $n(n-1)p^2$:

$$ E[X(X-1)] = n(n-1)p^2 \sum_{k=2}^{n} \frac{(n-2)!}{(k-2)!(n-k)!} p^{k-2} (1-p)^{n-k} $$

Again, this sum is over a binomial distribution $B(n-2, p)$, which equals 1:

$$ E[X(X-1)] = n(n-1)p^2 $$

Now I can get $E[X^2]$ using $E[X^2] = E[X(X-1)] + E[X]$:

$$ E[X^2] = n(n-1)p^2 + np $$

Finally, the variance:

$$ \text{Var}(X) = (n(n-1)p^2 + np) - (np)^2 $$

Let me expand this:

$$ = n^2p^2 - np^2 + np - n^2p^2 = np - np^2 $$

$$ \boxed{\text{Var}(X) = np(1-p)} $$

---

## What Does This Mean?

These results are beautifully simple. The mean $np$ makes perfect sense – it's literally the number of trials times the success rate.

The variance $np(1-p)$ is more interesting. Notice that when $p=0.5$, the variance is maximized at $0.25n$. When $p$ is close to 0 or 1, the variance shrinks – makes sense, because outcomes become more predictable. The $(1-p)$ term is sometimes written as $q$, giving us $npq$.

These formulas are the backbone of so many statistical tests and ML algorithms. Every time you see a logistic regression model or work with bernoulli processes, this distribution is lurking underneath.

Next, I want to explore how this connects to the Beta distribution – they have an interesting relationship when you start thinking about Bayesian priors for $p$!
