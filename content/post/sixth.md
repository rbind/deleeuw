+++
date = "2017-06-03T09:00:00"
draft = false
tags = []
title = "Majorization"
math = true
+++
I use majorization in many of my papers. So a short general introduction with some simple examples may be useful. Here we go.
<!--more-->

<h2>1 Introduction</h2>

The problem we try to solve throughout is to construct a convergent and stable iterative algorithm to minimize a function `$f:X\rightarrow\mathbb{R}$` over `$X\subseteq\mathbb{R}^n$`. 

A *majorization scheme* for `$f$` on `$X$` is a function `$g:X\otimes X\rightarrow\mathbb{R}$` such that

* `$g(x,y)\geq f(x)$` for all `$x,y\in X$`.
* `$g(x,x)=f(x)$` for all `$x\in X$`.

In other words `$f(x)=\min_{y\in X}g(x,y)$` and `$x\in\mathop{\text{argmin}}_{y\in X}g(x,y)$`. A majorization scheme is *strict* if `$g(x,y)<f(x)$` for all `$x\not =y$` in `$X$`. 

A majorization scheme generates an *iterative majorization algorithm* by the rule

<div>
  $$x^{(k+1)}\in\mathop{\text{argmin}}_{x\in X}g(x,x^{(k)}).$$
</div>

The key result in majorization theory is the *sandwich inequality*
<div>
$$f(x^{(k+1)})\leq g(x^{(k+1)},x^{(k)})\leq g(x^{(k)},x^{(k)})=f(x^{(k)}).$$
</div>

If the function `$f$` is bounded below, the iterates stay in a compact set, the majorization scheme is continuous, and all minima are attained at unique points, then we have convergence to a *fixed point* 
`$x_\infty\in X$`, i.e. a point with `$x_\infty=\mathop{\text{argmin}}_{x\in X}g(x,x_\infty)$`.
The assumptions for convergence can be relaxed a great deal, but we will not go into such details.

<h2>2 Tools of the Trade</h2>

<h3>2.1 Inequalities</h3>

<h3>2.2 Convexity</h3>

<h3>2.3 Taylor's Theorem</h3>

<h2>Example: The Weber Point</h2>

<h2>Example: Multidimensional Scaling</h2>

First we give an example in which a simple inequality is used to derive a majorization scheme. In
multidimensional scaling, or MDS, we minimize

<div>
$$\sigma(X)=\sum_{i=1}^n\sum_{j=1}^n w_{ij}(\delta_{ij}-d_{ij}(X))^2,$$
</div>

over all `$n\times p$` *configuration* matrices $X$. Here `$W=\{w_{ij}\}$` and `$\Delta=\{\delta_{ij}\}$`
are given symmetric and non-negative matries, with zeroes on the diagonal, and `$D(X)=\{d_{ij}(X)\}$`
is the matrix-valued function of Euclidean distances between the `$n$` points in `$\mathbb{R}^p$` with coordinates in the rows of `$X$`.

Now

<div>
$$d_{ij}(X)=\sqrt{\mathbf{tr}\ X'A_{ij}X},$$
</div>
   
where `$A_{ij}$` is a symmetric matrix of order `$n$` with elements `$(i,i)$` and `$(j,j)$` equal to +1
and elements `$(i,j)$` and `$(j,i)$` equal to -1. All other elements are zero.

<h2>Example: EM</h2>

<h2>Example: Logistic Regression</h2>

<script type="text/javascript"
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  tex2jax: {
    inlineMath: [['$','$'], ['\\(','\\)']],
    displayMath: [['$$','$$'], ['\[','\]']],
    processEscapes: true,
    processEnvironments: true,
    skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
    TeX: { equationNumbers: { autoNumber: "AMS" },
         extensions: ["AMSmath.js", "AMSsymbols.js"] }
  }
});
</script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Queue(function() {
    var all = MathJax.Hub.getAllJax(), i;
    for(i = 0; i < all.length; i += 1) {
        all[i].SourceElement().parentNode.className += ' has-jax';
    }
});
</script>
