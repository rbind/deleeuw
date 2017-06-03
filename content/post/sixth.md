+++
date = "2017-06-03T09:00:00"
draft = false
tags = []
title = "Majorization"
math = true
+++
I use majorization in many of my papers. So a short general introduction may be useful. 
<!--more-->

The problem we try to solve throughout is to construct a convergent and stable iterative algorithm to minimize a function `$f:X\rightarrow\mathbb{R}$` over a set `$X\subseteq\mathbb{R}^n$`. 

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

If the sequence `$f$` is bounded below, the iterates stay in a compact set, the majorization scheme is continuous, and all minima are attained and unique, then we have convergence to a *fixed point* 
`$x_\infty\in X$`, i.e. a point with `$x_\infty\in\mathop{\text{\argmin}}_{x\in X}g(x,x_\infty)$`.

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
