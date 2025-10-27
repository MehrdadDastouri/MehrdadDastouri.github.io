---
layout: post
title: "Deriving the Normal Equation for Linear Regression"
date: 2025-10-27 11:00:00 -0400
categories: machine-learning mathematics linear-regression
---

<!-- 
  The content below is injected directly into the post layout.
  The wrapping elements like <article> or post title are handled by the layout files.
-->
<p>
  Linear regression is often the first algorithm one encounters in machine learning. It's simple, interpretable, and forms the bedrock for many more complex models. The core idea is to find the "line of best fit" that minimizes the error between predicted and actual values. But how do we mathematically define and find this optimal line?
</p>
<p>
  The goal is to find the parameter vector $\boldsymbol{\theta}$ that minimizes the <strong>Sum of Squared Errors (SSE)</strong>. Today, we'll walk through the calculus to derive the famous "Normal Equation," which gives us a closed-form solution for these optimal parameters.
</p>

<p>Let's assume our model's prediction for a given data point $\mathbf{x}_n$ is linear:
  $$ \hat{y}_n = \boldsymbol{\theta}^T \mathbf{x}_n $$
</p>

<hr class="my-4">

<h3>Step 1: Define the Cost Function (Sum of Squared Errors)</h3>
<p>
  The error, or "residual," for a single data point is the difference between the actual value $y_n$ and the predicted value $\hat{y}_n$. We square these errors so that positive and negative errors don't cancel out, and to heavily penalize larger errors.
</p>
<p>
  The total cost function, $J(\boldsymbol{\theta})$, which we want to minimize, is the sum of these squared errors over all $N$ data points in our training set:
  $$ J(\boldsymbol{\theta}) = \sum_{n=1}^{N} (y_n - \hat{y}_n)^2 = \sum_{n=1}^{N} (y_n - \boldsymbol{\theta}^T \mathbf{x}_n)^2 $$
</p>

<h3>Step 2: Vectorize the Cost Function</h3>
<p>
  Working with summations can be cumbersome. We can express the cost function more cleanly using matrix and vector notation. Let's define:
</p>
<ul>
  <li>$\mathbf{y}$: a vector of all target values, $[y_1, y_2, \dots, y_N]^T$.</li>
  <li>$\mathbf{X}$: the "design matrix," where each row is a data point vector $\mathbf{x}_n^T$.</li>
  <li>$\boldsymbol{\theta}$: the parameter vector.</li>
</ul>
<p>
  With these, the vector of all predictions is $\mathbf{X}\boldsymbol{\theta}$, and the vector of all errors is $\mathbf{y} - \mathbf{X}\boldsymbol{\theta}$. The sum of squared errors is simply the squared Euclidean norm of this error vector:
  $$ J(\boldsymbol{\theta}) = \| \mathbf{y} - \mathbf{X}\boldsymbol{\theta} \|_2^2 = (\mathbf{y} - \mathbf{X}\boldsymbol{\theta})^T (\mathbf{y} - \mathbf{X}\boldsymbol{\theta}) $$
</p>

<hr class="my-4">

<h3>Step 3: Minimize the Cost by Taking the Gradient</h3>
<p>
  To find the value of $\boldsymbol{\theta}$ that minimizes $J(\boldsymbol{\theta})$, we need to compute its gradient with respect to $\boldsymbol{\theta}$ and set it to zero. First, let's expand the cost function:
  $$ J(\boldsymbol{\theta}) = (\mathbf{y}^T - \boldsymbol{\theta}^T\mathbf{X}^T) (\mathbf{y} - \mathbf{X}\boldsymbol{\theta}) $$
  $$ J(\boldsymbol{\theta}) = \mathbf{y}^T\mathbf{y} - \mathbf{y}^T\mathbf{X}\boldsymbol{\theta} - \boldsymbol{\theta}^T\mathbf{X}^T\mathbf{y} + \boldsymbol{\theta}^T\mathbf{X}^T\mathbf{X}\boldsymbol{\theta} $$
  Since $\boldsymbol{\theta}^T\mathbf{X}^T\mathbf{y}$ is a scalar, it's equal to its own transpose, $(\boldsymbol{\theta}^T\mathbf{X}^T\mathbf{y})^T = \mathbf{y}^T\mathbf{X}\boldsymbol{\theta}$. So we can combine the middle terms:
  $$ J(\boldsymbol{\theta}) = \mathbf{y}^T\mathbf{y} - 2\boldsymbol{\theta}^T\mathbf{X}^T\mathbf{y} + \boldsymbol{\theta}^T\mathbf{X}^T\mathbf{X}\boldsymbol{\theta} $$
  Now, we take the gradient with respect to $\boldsymbol{\theta}$ using standard matrix calculus rules:
  $$ \nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta}) = \nabla_{\boldsymbol{\theta}} (\mathbf{y}^T\mathbf{y} - 2\boldsymbol{\theta}^T\mathbf{X}^T\mathbf{y} + \boldsymbol{\theta}^T\mathbf{X}^T\mathbf{X}\boldsymbol{\theta}) $$
  $$ \nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta}) = \mathbf{0} - 2\mathbf{X}^T\mathbf{y} + 2\mathbf{X}^T\mathbf{X}\boldsymbol{\theta} $$
</p>

<h3>Step 4: Solve for the Optimal Parameters $\hat{\boldsymbol{\theta}}$</h3>
<p>
  Setting the gradient to the zero vector gives us the minimum:
  $$ -2\mathbf{X}^T\mathbf{y} + 2\mathbf{X}^T\mathbf{X}\hat{\boldsymbol{\theta}} = \mathbf{0} $$
  Where $\hat{\boldsymbol{\theta}}$ denotes the optimal parameter vector. Simplifying this gives the well-known Normal Equation in matrix form:
  $$ \mathbf{X}^T\mathbf{X}\hat{\boldsymbol{\theta}} = \mathbf{X}^T\mathbf{y} $$
</p>

<h4>Connecting to the Problem's Equation</h4>
<p>
  The equation in the problem statement is presented using summations. Let's show that our matrix form is identical. The term $\mathbf{X}^T\mathbf{X}$ is:
  $$ \mathbf{X}^T\mathbf{X} = \sum_{n=1}^{N} \mathbf{x}_n \mathbf{x}_n^T $$
  And the term $\mathbf{X}^T\mathbf{y}$ is:
  $$ \mathbf{X}^T\mathbf{y} = \sum_{n=1}^{N} \mathbf{x}_n y_n = \sum_{n=1}^{N} y_n \mathbf{x}_n $$
  Substituting these back into our matrix equation, we get:
  $$ \left( \sum_{n=1}^{N} \mathbf{x}_n \mathbf{x}_n^T \right) \hat{\boldsymbol{\theta}} = \sum_{n=1}^{N} y_n \mathbf{x}_n $$
  This is precisely the equation (3.13) we were asked to prove.
</p>

<hr class="my-4">

<h4>Conclusion</h4>
<p>
  We have successfully proven that by minimizing the sum of squared errors, we arrive at the Normal Equation. This provides an elegant, analytical solution for the optimal parameters in a linear regression model, denoted as $\hat{\boldsymbol{\theta}}$. By solving this system of linear equations, often written as $\hat{\boldsymbol{\theta}} = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y}$, we can directly compute the best-fit parameters without needing iterative methods like gradient descent.
</p>

پس از جایگزین کردن محتوای فایل پست، سایت را دوباره بیلد کنید. این بار، محتوای پست "Least Squares" باید به درستی و به صورت کامل زیر عنوانش در صفحه وبلاگ نمایش داده شود.

---
**نکته مهم:** خطای `LiquidHTMLParsingError` در `_includes/project_preview.liquid` همچنان وجود دارد و مانع بیلد شدن سایت شما می‌شود. بعد از اینکه این مشکل نمایش پست را حل کردید، باید به سراغ آن برویم. لطفاً محتوای آن فایل را برایم بفرستید تا اصلاحش کنیم.
