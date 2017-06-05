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

In this section we will try to give some idea of the tools that are available to construct majorization schemes and the corresponding majorization algorithms.

<h3>2.1 Inequalities</h3>

Any inequality of the form `$h(x,y)\geq f(x)+f(y)$`, with equality if and only if 
`$x=y$` leads to a strict majorization scheme with `$g(x,y)=h(x,y)-f(y)$`. This
also covers inequalities of the form `$h(x,y)\leq f(x)+f(y)$` by multiplying
by -1 and inequalities of the form `$h(x,y)\geq f(x)f(y)$` (with positive functions) 
by taking logarithms.

<h4>2.1.1 AM/GM</h4>

Consider, for example, minimization of 

<div>
  $$f(x)=\sum_{i=1}^n w_i\sqrt{h_i(x)},$$
</div>

where the `$h_i(x)=x'A_ix-2x'b_i+c_i$` and we assume the quadratics `$h_i(x)$` are positive for all `$x$`. This has as a special case the Weber problem of locating a point `$x$` at minimum weighted distance fom a number of given points `$z_i$`. In statistics it is also known as computing the multivariate median.

The AM-GM inequality says

<div>
  $$\sqrt{h_i(x)}\sqrt{h_i(y)}\leq\frac12\{h_i(x)+h_i(y)\},$$
</div>

and thus `$f(x)\leq g(x,y)$` with a majorization scheme

<div>
  $$g(x,y)=\sum_{i=1}^n\frac{w_i}{h_i(y)}\{h_i(x)+h_i(y)\},$$
</div>

which is quadratic in `$x$`, and thus easy to minimize. The majorization algorithm is

<div>
$$x^{(k+1)}=\left\{\sum_{i=1}^n \frac{w_i}{h_i(x^{(k)})}A_i\right\}^{-1}\sum_{i=1}^n w_i\frac{w_i}{h_i(x^{(k)})}b_i.$$
</div>  

<h4>2.1.2 Cauchy-Schwartz</h4>

In multidimensional scaling, or MDS, we minimize a function of the form

<div>
$$f(x)=\sum_{i=1}^n w_i(\delta_i-\sqrt{x'A_ix})^2,$$
</div>

where again the $A_i$ are positive semi-definite. Suppose without loss of generalitythe `$\delta_i$` have weighted sum of squares equal to 1. Then

<div>
$$f(x)=1+x'Vx-2\sum_{i=1}^n w_i\delta_i\sqrt{x'A_ix},$$
</div>

with

<div>
  $$V=\sum_{i=1}^n w_iA_i.$$
</div>

The Cauchy-Schwartz inequality gives

<div>
$$\sqrt{x'A_ix}\sqrt{y'A_iy}\leq x'A_iy$$
</div>

and thus we have a majorization scheme defined by

<div>
  $$g(x,y)=1+x'Vx-2x'B(y)y,$$
</div>
   
with

<div>
  $$B(y)=\sum_{i=1}^n \frac{w_i}{\sqrt{y'A_iy}}A_i.$$
</div>

The majorization algorithm is

<div>
  $$x^{(k+1)}=V^+B(x^{(k)})x^{(k)}.$$
</div>

<h4>2.1.3 Jensen</h4>

Suppose `$-\infty=a_0<a_1<\cdots<a_n<a_{m+1}=+\infty$` are numbers that partition the real line into `$(m+1)$` intervals. Suppose that a discrete random variable takes the values `$1,\cdots,m+1$` with probabilities

<div>
  $$\pi_j(\mu,\sigma)=\int_{a_{j-1}}^{a_j}\phi(x,\mu,\sigma)dx,$$
</div>

with

<div>
  $$\phi(x,\mu,\sigma)=\frac{1}{\sigma\sqrt{2\pi}}\exp\left\{-\frac12\left(\frac{x-\mu}{\sigma}\right)^2\right\}.$$
</div>

From a random sample of size `$n$` we have observed proportions `$p_j$`, which gives a log-likelihood

<div>
$$f(\mu,\sigma)=\sum_{j=1}^{m+1}p_j\log\pi_j(\mu,\sigma).$$
</div>

We will now use Jensen's inequality in the form

<div>
$$\log\frac{\int\phi(x,\widehat\mu,\widehat\sigma)\frac{\phi(x,\mu,\sigma)}{\phi(x,\widehat\mu,\widehat\sigma)}dx}{\int\phi(x,\widehat\mu,\widehat\sigma) dx}\geq
\frac{\int\phi(x,\widehat\mu,\widehat\sigma)\log\frac{\phi(x,\mu,\sigma)}{\phi(x,\widehat\mu,\widehat\sigma)}dx}{\int\phi(x,\widehat\mu,\widehat\sigma)dx}$$
</div>

which gives

<div>
\begin{multline*}
f(\mu,\sigma)\geq f(\widehat\mu,\widehat\sigma)+\\\sum_{j=1}^{m+1}\frac{p_j}{\pi_j(\widehat\mu,\widehat\sigma)}
\left\{\int_{a_{j-1}}^{a_j}\phi(x,\widehat\mu,\widehat\sigma)\log\phi(x,\mu,\sigma)dx-\int_{a_{j-1}}^{a_j}\phi(x,\widehat\mu,\widehat\sigma)\log\phi(x,\widehat\mu,\widehat\sigma)dx\right\}.
\end{multline*}
</div>

It follows that instep $k$ of the majorization algorithm we minimize 

<div>
  $$\log\sigma^2+\frac{1}{\sigma^2}\sum_{j=1}^{m+1} p_j(V_j^{(k)}+(E_j^{(k)}-\mu)^2),$$
</div>

where `$E_j^{(k)}$` and `$V_j^{(k)}$` are the mean and variance of the truncated normal on `$(a_{j-1},a_j)$` with parameters 
$\mu^{(k)}$ and $\sigma^{(k)}$. The minimizers are

<div>
$$\mu^{(k+1)}=\sum_{j=1}^{m+1}p_jE_j^{(k)},$$
</div>

and

<div>
$$(\sigma^2)^{(k+1)}=\sum_{j=1}^{m+1}p_j\left(V_j^{(k)}+(E_j^{(k)}-\mu^{(k+1)})^2\right).$$
</div>

In this case the majorization algorithm gives the same results as the EM algorithm, which is not surprising because EM algorithms are majorization algorithms based on Jensen's inequality.
<h3>2.2 Convexity</h3>

<h3>2.3 Taylor's Theorem</h3>

<h2>Example: The Weber Point</h2>

<h2>Example: Multidimensional Scaling</h2>

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
