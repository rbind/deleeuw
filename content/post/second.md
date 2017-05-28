+++
date = "2017-05-16T10:10:00"
draft = false
tags = []
title = "Just Some Equation"
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

MathJax works on this blog. **Proof:** Define

 `$$\Phi(x):=\frac{1}{\sqrt{2\pi}}\int_{-\infty}^x\exp\{-\frac12 z^2\}dz,$$`

and thus

 `$$\mathcal{D}\Phi(x)=\frac{1}{\sqrt{2\pi}}\exp\{-\frac12 x^2\}.$$`

 **QED**



