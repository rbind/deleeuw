+++
date = "2017-06-03T09:00:00"
draft = false
tags = []
title = "Majorization"
math = true
+++
I use majorization in many of my papers. So maybe a short general introduction is useful. 
I use majorization in many of my papers. So maybe a short general introduction is useful. 
I use majorization in many of my papers. So maybe a short general introduction is useful. 
I use majorization in many of my papers. So maybe a short general introduction is useful. 
I use majorization in many of my papers. So maybe a short general introduction is useful. 
<!--more-->

The problem we try to solve is to construct a convergent and stable iterative algorithm to minimize a function 
`$f$` over a set `$X$`. 

An *iterative algorithm* on a set `$X$` is a triple `$\langle\mathcal{A},S,f\rangle$`. Here `$\mathcal{A}:X\rightarrow 2^X$` is the *update map*, `$S\subseteq X$` are the *targets*, and `$f:X\rightarrow\mathbb{R}$` is the *evaluation function*.

An *iterative algorithm* generates a sequence, starting with `$x^{0}$`, by the rule
<div>
$$x^{(k+1)}\in A(x^{(k)})$$
</div>

<div>
$$\text{if }x\in S\text{ then }x\in\mathcal{A}(x)$$
</div>
An algorithm is *stable* if
<div>
$$f(A(x))\leq f(x)\text{ for all }x\in X$$ 
</div>

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
