+++
date = "2017-05-21T00:00:00"
draft = false
tags = []
title = "Simulaneous Diagonalization"
math = true
+++
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

We give necessary and sufficient conditions for solvability of `$A_j=XW_jX^T$`, with the `$A_j$` are m given positive semi-definite matrices of order `$n$`. The solution `$X$` is `$n\times p$` and the $m$ solutions `$W_j$` are required to be diagonal, positive semi-definite, and adding up to the identity. We do not require that `$p\leq n$`.

