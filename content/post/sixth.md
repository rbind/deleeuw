+++
date = "2017-06-03T09:00:00"
draft = false
tags = []
title = "Majorization"
math = true
+++
I use majorization in many of my papers. So maybe a short general introduction is useful. 
<!--more-->

The problem we try to solve throughout is to construct a convergent and stable iterative algorithm to minimize a function `$f:X\rightarrow\mathbb{R}$` over a set `$X\subseteq\mathbb{R}^n$`. 

A *majorization scheme* for `$f$` on `$X$` is a function `$g:X\otimes X\rightarrow\mathbb{R}$` such that

* `$g(x,y)\geq f(x)$` for all `$x,y\in X$`.
* `$g(x,x)=f(x)$` for all `$x\in X$`.

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
