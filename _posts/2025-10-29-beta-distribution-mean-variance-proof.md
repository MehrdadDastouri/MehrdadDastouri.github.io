---
layout: post
title: Beta Distribution Proof
date: 2025-10-29 10:00:00 -0330
description: Derivation of the Beta distribution from two Gamma distributions.
tags: math probability
categories: math
giscus_comments: true
related_posts: false
---

<div class="lead">
This post demonstrates how the Beta distribution can be derived from two Gamma-distributed random variables.
</div>

### Introduction

The Beta distribution is a continuous probability distribution defined on the interval $$[0, 1]$$. It is parameterized by two positive shape parameters, denoted by $$\alpha$$ and $$\beta$$. A key property is its relationship with the Gamma distribution.

If $$X \sim \text{Gamma}(\alpha, 1)$$ and $$Y \sim \text{Gamma}(\beta, 1)$$ are independent random variables, then the random variable $$U = \frac{X}{X+Y}$$ follows a Beta distribution with parameters $$\alpha$$ and $$\beta$$.

$$
U = \frac{X}{X+Y} \sim \text{Beta}(\alpha, \beta)
$$

This post will walk through the proof of this property.

### Proof

Let's define two new random variables:
$$
U = \frac{X}{X+Y} \quad \text{and} \quad V = X+Y
$$
To find the joint probability density function (PDF) of $$(U, V)$$, we first need to express $$X$$ and $$Y$$ in terms of $$U$$ and $$V$$:
$$
X = UV \quad \text{and} \quad Y = V - X = V - UV = V(1-U)
$$
Since $$X > 0$$ and $$Y > 0$$, we have $$UV > 0$$ and $$V(1-U) > 0$$. As $$V=X+Y$$, $$V$$ must be positive, which implies $$U > 0$$ and $$1-U > 0$$. Therefore, $$0 < U < 1$$ and $$V > 0$$.

Next, we calculate the Jacobian of the transformation:
$$
J = \det \begin{pmatrix} \frac{\partial x}{\partial u} & \frac{\partial x}{\partial v} \\ \frac{\partial y}{\partial u} & \frac{\partial y}{\partial v} \end{pmatrix} = \det \begin{pmatrix} v & u \\ -v & 1-u \end{pmatrix} = v(1-u) - u(-v) = v - vu + vu = v
$$
The absolute value of the Jacobian is $$|J| = |v| = v$$, since $$v>0$$.

The joint PDF of $$X$$ and $$Y$$ is the product of their individual PDFs, as they are independent:
$$
f_{X,Y}(x,y) = f_X(x) f_Y(y) = \frac{x^{\alpha-1}e^{-x}}{\Gamma(\alpha)} \frac{y^{\beta-1}e^{-y}}{\Gamma(\beta)}
$$
Now, we can find the joint PDF of $$(U, V)$$ using the change of variables formula:
$$
f_{U,V}(u,v) = f_{X,Y}(uv, v(1-u)) \cdot |J|
$$
$$
f_{U,V}(u,v) = \frac{(uv)^{\alpha-1}e^{-uv}}{\Gamma(\alpha)} \frac{(v(1-u))^{\beta-1}e^{-v(1-u)}}{\Gamma(\beta)} \cdot v
$$
Let's simplify this expression:
$$
f_{U,V}(u,v) = \frac{u^{\alpha-1}v^{\alpha-1} \cdot v^{\beta-1}(1-u)^{\beta-1}}{\Gamma(\alpha)\Gamma(\beta)} e^{-uv} e^{-v+uv} \cdot v
$$
$$
f_{U,V}(u,v) = \frac{u^{\alpha-1}(1-u)^{\beta-1}}{\Gamma(\alpha)\Gamma(\beta)} v^{\alpha-1+\beta-1+1} e^{-v}
$$
$$
f_{U,V}(u,v) = \frac{u^{\alpha-1}(1-u)^{\beta-1}}{\Gamma(\alpha)\Gamma(\beta)} v^{\alpha+\beta-1} e^{-v}
$$
This is the joint PDF for $$U$$ and $$V$$. To find the marginal PDF of $$U$$, we integrate out $$V$$ over its domain $$(0, \infty)$$:
$$
f_U(u) = \int_0^\infty f_{U,V}(u,v) \,dv = \int_0^\infty \frac{u^{\alpha-1}(1-u)^{\beta-1}}{\Gamma(\alpha)\Gamma(\beta)} v^{\alpha+\beta-1} e^{-v} \,dv
$$
The term $$ \frac{u^{\alpha-1}(1-u)^{\beta-1}}{\Gamma(\alpha)\Gamma(\beta)} $$ is constant with respect to $$v$$, so we can pull it out of the integral:
$$
f_U(u) = \frac{u^{\alpha-1}(1-u)^{\beta-1}}{\Gamma(\alpha)\Gamma(\beta)} \int_0^\infty v^{\alpha+\beta-1} e^{-v} \,dv
$$
The integral is the definition of the Gamma function $$\Gamma(\alpha+\beta)$$:
$$
\int_0^\infty v^{(\alpha+\beta)-1} e^{-v} \,dv = \Gamma(\alpha+\beta)
$$
Substituting this back, we get:
$$
f_U(u) = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} u^{\alpha-1}(1-u)^{\beta-1}
$$
This is precisely the PDF of a Beta distribution with parameters $$\alpha$$ and $$\beta$$, defined for $$0 < u < 1$$.

This completes the proof.
