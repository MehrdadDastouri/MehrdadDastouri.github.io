---
layout: post
title: "Moments of the Dirichlet Distribution: Mean, Variance, and Covariance"
date: 2025-11-02 09:00:00 -0400
categories: statistics probability
tags: math multivariate-statistics dirichlet-distribution
---

<p>
  After exploring the Beta distribution, a natural next step is to investigate its multivariate generalization: the Dirichlet distribution. The Dirichlet distribution is a family of continuous multivariate probability distributions parameterized by a vector $\mathbf{a}$ of positive reals. It is often used as a prior distribution in Bayesian statistics, particularly for the parameters of a categorical or multinomial distribution.
</p>
<p>
  A random vector $\mathbf{x} = (x_1, \dots, x_K)$ follows a Dirichlet distribution, denoted $\mathbf{x} \sim \text{Dir}(\mathbf{a})$, if its probability density function (PDF) is defined over the standard $K-1$ simplex (where $x_k > 0$ for all $k$ and $\sum_{k=1}^K x_k = 1$):
  $$ f(\mathbf{x}; \mathbf{a}) = \frac{1}{B(\mathbf{a})} \prod_{k=1}^K x_k^{a_k-1} $$
  The normalizing constant is the multivariate Beta function, $B(\mathbf{a}) = \frac{\prod_{k=1}^K \Gamma(a_k)}{\Gamma(\sum_{k=1}^K a_k)}$. Let's define $\bar{a} = \sum_{k=1}^K a_k$ for simplicity, which matches the notation in our target problem. The PDF is then:
  $$ f(\mathbf{x}; \mathbf{a}) = \frac{\Gamma(\bar{a})}{\prod_{k=1}^K \Gamma(a_k)} \prod_{k=1}^K x_k^{a_k-1} $$
  Our objective is to derive the mean $E[x_k]$, the variance $\sigma_{x_k}^2$, and the covariance $\text{cov}[x_i, x_j]$ for this distribution.
</p>

<hr class="my-4">

<h3>Part 1: Deriving the Mean ($E[x_k]$)</h3>
<p>
  The expected value of any component $x_k$ is found by integrating $x_k$ against the PDF over the entire support (the simplex $\mathcal{S}_K$).
  $$ E[x_k] = \int_{\mathcal{S}_K} x_k \cdot \frac{\Gamma(\bar{a})}{\prod_{j=1}^K \Gamma(a_j)} \left( \prod_{j=1}^K x_j^{a_j-1} \right) d\mathbf{x} $$
  We can move the constant term outside and absorb $x_k$ into the product:
  $$ E[x_k] = \frac{\Gamma(\bar{a})}{\prod_{j=1}^K \Gamma(a_j)} \int_{\mathcal{S}_K} x_k^{a_k} \prod_{j \neq k} x_j^{a_j-1} \,d\mathbf{x} $$
  The expression inside the integral is the kernel of another Dirichlet distribution. Let's define a new parameter vector $\mathbf{a}'$ where $a'_k = a_k+1$ and $a'_j = a_j$ for $j \neq k$. The sum of these new parameters is $\bar{a}' = (\bar{a}-a_k) + (a_k+1) = \bar{a}+1$.
  The integral is therefore the normalizing constant for a $\text{Dir}(\mathbf{a}')$ distribution:
  $$ \int_{\mathcal{S}_K} \prod_{j=1}^K x_j^{a'_j-1} \,d\mathbf{x} = B(\mathbf{a}') = \frac{\Gamma(a_k+1) \prod_{j \neq k} \Gamma(a_j)}{\Gamma(\bar{a}+1)} $$
  Substituting this back into the equation for $E[x_k]$:
  $$ E[x_k] = \frac{\Gamma(\bar{a})}{\prod_{j=1}^K \Gamma(a_j)} \cdot \frac{\Gamma(a_k+1) \prod_{j \neq k} \Gamma(a_j)}{\Gamma(\bar{a}+1)} $$
  Using the property $\Gamma(z+1)=z\Gamma(z)$, we can simplify $\Gamma(a_k+1) = a_k\Gamma(a_k)$ and $\Gamma(\bar{a}+1) = \bar{a}\Gamma(\bar{a})$. Many terms cancel out:
  $$ E[x_k] = \frac{\Gamma(\bar{a})}{\Gamma(a_k) \prod_{j \neq k} \Gamma(a_j)} \cdot \frac{a_k \Gamma(a_k) \prod_{j \neq k} \Gamma(a_j)}{\bar{a}\Gamma(\bar{a})} = \frac{a_k}{\bar{a}} $$
  This gives us the mean for any component $x_k$.
  $$ E[x_k] = \frac{a_k}{\bar{a}} $$
</p>

<h3>Part 2: Deriving the Second Moments ($E[x_k^2]$ and $E[x_i x_j]$)</h3>
<p>
  To find the variance and covariance, we first need the second-order moments. We use the same technique.
  <br><br>
  <strong>For $E[x_k^2]$:</strong>
  $$ E[x_k^2] = \int_{\mathcal{S}_K} x_k^2 \cdot f(\mathbf{x}; \mathbf{a}) \,d\mathbf{x} = \frac{\Gamma(\bar{a})}{\prod_{j=1}^K \Gamma(a_j)} \int_{\mathcal{S}_K} x_k^{a_k+1} \prod_{j \neq k} x_j^{a_j-1} \,d\mathbf{x} $$
  The integral corresponds to a Dirichlet with parameters $(a_1, \dots, a_k+2, \dots, a_K)$. The sum of these parameters is $\bar{a}+2$. The integral evaluates to:
  $$ \frac{\Gamma(a_k+2) \prod_{j \neq k} \Gamma(a_j)}{\Gamma(\bar{a}+2)} $$
  So, the expectation is:
  $$ E[x_k^2] = \frac{\Gamma(\bar{a})}{\Gamma(a_k)} \cdot \frac{\Gamma(a_k+2)}{\Gamma(\bar{a}+2)} = \frac{\Gamma(\bar{a})}{\Gamma(a_k)} \cdot \frac{(a_k+1)a_k\Gamma(a_k)}{(\bar{a}+1)\bar{a}\Gamma(\bar{a})} = \frac{a_k(a_k+1)}{\bar{a}(\bar{a}+1)} $$
  <br>
  <strong>For $E[x_i x_j]$ where $i \neq j$:</strong>
  $$ E[x_i x_j] = \frac{\Gamma(\bar{a})}{\prod_{k=1}^K \Gamma(a_k)} \int_{\mathcal{S}_K} x_i^{a_i} x_j^{a_j} \prod_{k \neq i,j} x_k^{a_k-1} \,d\mathbf{x} $$
  This integral corresponds to a Dirichlet with parameters updated at two positions: $a_i+1$ and $a_j+1$. The sum is again $\bar{a}+2$. The integral is:
  $$ \frac{\Gamma(a_i+1)\Gamma(a_j+1) \prod_{k \neq i,j} \Gamma(a_k)}{\Gamma(\bar{a}+2)} $$
  Thus, the expectation is:
  $$ E[x_i x_j] = \frac{\Gamma(\bar{a})}{\Gamma(a_i)\Gamma(a_j)} \cdot \frac{\Gamma(a_i+1)\Gamma(a_j+1)}{\Gamma(\bar{a}+2)} = \frac{\Gamma(\bar{a})}{\Gamma(a_i)\Gamma(a_j)} \cdot \frac{a_i\Gamma(a_i)a_j\Gamma(a_j)}{(\bar{a}+1)\bar{a}\Gamma(\bar{a})} = \frac{a_i a_j}{\bar{a}(\bar{a}+1)} $$
</p>

<h3>Part 3: Deriving Variance and Covariance</h3>
<p>
  Now we can use the standard formulas with the moments we've just found.
  <br><br>
  <strong>Variance $\sigma_{x_k}^2$:</strong>
  $$ \sigma_{x_k}^2 = \text{Var}(x_k) = E[x_k^2] - (E[x_k])^2 = \frac{a_k(a_k+1)}{\bar{a}(\bar{a}+1)} - \left(\frac{a_k}{\bar{a}}\right)^2 $$
  Finding a common denominator of $\bar{a}^2(\bar{a}+1)$:
  $$ \text{Var}(x_k) = \frac{a_k(a_k+1)\bar{a} - a_k^2(\bar{a}+1)}{\bar{a}^2(\bar{a}+1)} = \frac{a_k^2\bar{a} + a_k\bar{a} - a_k^2\bar{a} - a_k^2}{\bar{a}^2(\bar{a}+1)} $$
  $$ = \frac{a_k\bar{a} - a_k^2}{\bar{a}^2(\bar{a}+1)} = \frac{a_k(\bar{a}-a_k)}{\bar{a}^2(\bar{a}+1)} $$
  Matching the problem's notation, this is:
  $$ \sigma_{x_k}^2 = \frac{a_k(\bar{a}-a_k)}{\bar{a}^2(1+\bar{a})} $$
  <br>
  <strong>Covariance $\text{cov}[x_i, x_j]$:</strong>
  $$ \text{cov}[x_i, x_j] = E[x_i x_j] - E[x_i]E[x_j] = \frac{a_i a_j}{\bar{a}(\bar{a}+1)} - \left(\frac{a_i}{\bar{a}}\right)\left(\frac{a_j}{\bar{a}}\right) $$
  Using the same common denominator:
  $$ \text{cov}[x_i, x_j] = \frac{a_i a_j \bar{a} - a_i a_j (\bar{a}+1)}{\bar{a}^2(\bar{a}+1)} = \frac{a_i a_j \bar{a} - a_i a_j \bar{a} - a_i a_j}{\bar{a}^2(\bar{a}+1)} $$
  $$ = \frac{-a_i a_j}{\bar{a}^2(\bar{a}+1)} $$
  Again, matching the requested format:
  $$ \text{cov}[x_i, x_j] = -\frac{a_i a_j}{\bar{a}^2(1+\bar{a})} $$
</p>
