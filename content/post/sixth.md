+++
date = "2017-06-06T09:00:00"
draft = false
tags = []
title = "Majorization in a Nutshell"
math = true
+++
I use majorization in many of my papers. So a relatively short general introduction with some examples may be useful. Here we go.
Keep reading. If the math looks weird, refresh your browser.
<!--more-->

<h2>1 Introduction</h2>

The problem we try to solve throughout is to construct a convergent and stable iterative algorithm to minimize a function 
`$f:X\rightarrow\mathbb{R}$` over `$X\subseteq\mathbb{R}^n$`. 

<h3>1.1 Majorization</h3>

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
`$x_\infty\in X$`, i.e. a point with `$x_\infty=\mathop{\text{argmin}}_{x\in X}g(x,x_\infty)$`. More precisely, the sequence
`$f(x^{(k)})$` converges, each accumulation point of the sequence `$x^{(k)}$` we generate is a fixed point, and all accumulation points have the same function value. The assumptions for convergence can be relaxed a great deal, but we will not specify these in detail.

Finally, note that we use majorization for minimization problems. In the same way we can use minorization for maximization problems. This is the reason majorization algorithms are usually called MM algorithms these days.

<h3>1.2 Differentiable Functions</h3>

Suppose `$X$` is the whole of `$\mathbb{R}^n$`, and `$f$` and `$g$` are differentiable at a fixed point `$x$`. Then `$\mathcal{D}_1g(x,x)=\mathcal{D}f(x)$` and if `$f$` and `$g$` are twice differentiable `$\mathcal{D}_{11}g(x,x)\gtrsim\mathcal{D}^2f(x)$` in the 
Loewner sense. This follows from the fact that `$g(x,y)-f(x)$` attains its minimum, equal to zero, over `$x\in X$` at `$x=y$`. 
In fact the majorization relation implies that `$\mathcal{D}^2f(x)=\mathcal{D}_{11}g(x,x)+\mathcal{D}_{12}g(x,x)$` and
`$\mathcal{D}_{21}g(x,x)+\mathcal{D}_{22}g(x,x)=0$` for all `$x$`.

If `$A$` is the algorithmic map that computes the successor of `$y$`, i.e. `$A(y)=\mathop{\text{argmin}}_{x\in X}g(x,y)$`, then

<div>
  $$\mathcal{D}A(x)=-[\mathcal{D}_{11}g(x,x)]^{-1}\mathcal{D}_{12}g(x,x)=I-[\mathcal{D}_{11}g(x,x)]^{-1}\mathcal{D}^2f(x)$$
</div>

If the spectral norm `$\rho(x)$`, the eigenvalue of largest modulus, of `$\mathcal{D}A(x)$` is strictly between zero and one, then
the majorization algorithm converges linearly with rate `$\rho(x)$`.

<h2>2 Tools of the Trade</h2>

In this section we will try to give some idea of the tools that are available to construct majorization schemes and of the corresponding majorization algorithms they generate.

<h3>2.1 Inequalities</h3>

Any inequality of the form `$h(x,y)\geq f(x)+f(y)$`, with equality if and only if 
`$x=y$` leads to a strict majorization scheme with `$g(x,y)=h(x,y)-f(y)$`. This
also covers inequalities of the form `$h(x,y)\leq f(x)+f(y)$` by multiplying
by -1, and inequalities of the form `$h(x,y)\geq f(x)f(y)$` (with positive functions) 
by taking logarithms.

<h4>2.1.1 AM/GM Inequality</h4>

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
$$x^{(k+1)}=\left\{\sum_{i=1}^n \frac{w_i}{h_i(x^{(k)})}A_i\right\}^{-1}\sum_{i=1}^n \frac{w_i}{h_i(x^{(k)})}b_i.$$
</div>  

<h4>2.1.2 Cauchy-Schwartz Inequality</h4>

In multidimensional scaling, or MDS, we minimize a function of the form

<div>
$$f(x)=\sum_{i=1}^n w_i(\delta_i-\sqrt{x'A_ix})^2,$$
</div>

where again the $A_i$ are positive semi-definite. Suppose without loss of generality the `$\delta_i$` have weighted sum of squares equal to 1. Then

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

<h4>2.1.3 Jensen's Inequality</h4>

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

It follows that in step $k$ of the majorization algorithm we minimize 

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

Instead of specific inequalities we can also base majorization schemes on more general tools, such as properties of convex or concave functions. If $f$ is concave, for example,

<div>
  $$f(x)\leq f(y)+(x-y)'z,$$
</div>

for any `$z\in\partial f(y)$`, the subgradient at `$y$`. This is known as *tangential minorization*, because a concave function
is below any of its tangents, in the same way as a convex function is above its tangents.

<h4>2.2.1 Aspects</h4>

Suppose `$\mathcal{K}_j$`, for `$j=1,\cdots,m$`, are convex cones in `$\mathbb{R}^n$`. Cone `$\mathcal{K}_j$` defines the possible transformations of `$n$` observations on variable `$j$`. Also `$\mathcal{S}$` is the unit sphere in `$\mathbb{R}^n$`.

Given `$x_j\in\mathcal{K}_j\cap\mathcal{S}$` we can compute the correlation matrix `$R(x)=\{r_{j\ell}(x)\}=\{x_j'x_\ell\}$`. Now suppose

<div>
$$f(x)=h(R(x))$$
</div>

where `$h$` is a convex real-valued function on the space of correlation matrices, which we call an *aspect*. Multivariate analysis abounds with convex gain functions, such as the sum of the $p$ largest eigenvalues, the negative log-determinant, the squared multiple correlation of one variable with the others, and the maximum of the multinormal log-likelihood.

By concavity

<div>
$$f(x)\geq f(y)+\mathbf{tr}\ G(y)(R(x)-R(y)),$$
</div>

with `$G(y)\in\partial h(y)$.` Thus we have a minorization scheme and the minorization algorithm maximizes the quadratic

<div>
  $$\sum_{j=1}^m\sum_{\ell=1}^m g_{j\ell}(x^{(k)})x_j'x_\ell^{\ }$$
</div>

over the `$x_j\in\mathcal{K}_j\cap\mathcal{S}$`. Computing transformed variables in this way is sometimes known as *optimal scaling*.

<h4>2.2.2 Tomography</h4>

We can use the definition of convexity directly to majorize `$f$` by a separable majorization scheme, a weighted sum of functions of one variable. Suppose the function `$f$` we must minimize is defined by 

<div>
$$f(x)=h\left(\sum_{i=1}^n w_ix_i\right),$$
</div>

where `$h$` is a convex function of a single variable, and `$w$` is a vector of positive numbers.

If `$y$` is another vector of `$n$` positive numbers we can write 

<div>
$$f(x)=h\left(\sum_{i=1}^n \left(\frac{w_iy_i}{w'y}\right)\left(\frac{w'y}{y_i}x_i\right)\right),$$
</div>

and if `$g$` is defined as 

<div>
$$g(x,y)=\sum_{i=1}^n\left(\frac{w_iy_i}{w'y}\right)h\left(\frac{w'y}{y_i}x_i\right)$$
</div>

then, by the definition of convexity, `$f(x)\leq g(x,y)$`. Also, clearly, `$f(x)=g(x,x)$` and thus we have us a separable majorization scheme. 


Alternatively, for any positive vector `$\pi$` with elements adding up to one, 

<div>
$$f(x)=h\left(\sum_{i=1}^n\pi_i\left(\frac{w_i}{\pi_i}(x_i-y_i)-w'y\right)\right),$$
</div>

and the majorization scheme is defined as

<div>
$$g(x,y)=\sum_{i=1}^n\pi_ih\left(\frac{w_i}{\pi_i}(x_i-y_i)-w'y\right).$$
</div>

<h3>2.3 Taylor's Theorem</h3>

Another, even more general tool, is Taylor's theorem for a sufficiently many times differentiable function.

<h4>2.3.2 Second Order</h4>

If we use the Langrange form of the remainder we can write

<div>
  $$f(x)=f(y)+(x-y)'Df(y)+\frac12 (x-y)'D^2f(\xi)(x-y)$$
</div>

for some `$\xi$` on the line connecting `$x$` and `$y$`. Thus

<div>
  $$f(x)\leq f(y)+(x-y)'Df(y)+\frac12 \max_{0\leq\lambda\leq 1}(x-y)'D^2f(\lambda x +(1-\lambda)y)(x-y)$$
</div>

gives a majorization scheme, but the scheme may not be simple to minimize. If, however, `$\mathcal{D}^2f(x)\lesssim A$` for all
`$x\in X$` then the majorization scheme can be chosen as the quadratic

<div>
  $$f(x)\leq f(y)+(x-y)'Df(y)+\frac12(x-y)'A(x-y),$$
</div>

and the majorization algorithm is

<div>
$$x^{(k+1)}=\mathcal{P}_X(x^{(k)}-A^{-1}\mathcal{D}f(x^{(k)})),$$
</div>

with $\mathcal{P}$ the metric projection on `$X$`.

A simple example is logistic regression. The negative log-likelihood is

<div>
  $$f(x)=-\sum_{i=1}^n n_i\{p_i\log\pi_i(x)+(1-p_i)\log(1-\pi_i(x))\},$$
</div>

with

<div>
  $$\pi_i(x)=\frac{1}{1+\exp\{-z_i'x\}}.$$
</div>

This simplifies to

<div>
$$f(x)=\sum_{i=1}^n n_i\{p_iz_i'x-\log(1-\pi_i(x))\},$$
</div>

and thus

<div>
$$\mathcal{D}f(x)=\sum_{i=1}^n n_i\{p_i-\pi_i(x)\}z_i,$$
</div>

and

<div>
$$\mathcal{D}^2f(x)=\sum_{i=1}^nn_i\pi_i(x)(1-\pi_i(x))z_i^{\ }z_i'.$$
</div>

Now `$\pi_i(x)(1-\pi_i(x))\leq\frac14$`, and thus

<div>
$$\mathcal{D}^2f(x)\lesssim\frac14 Z'NZ.$$
</div> 

This simple bound can be used to get a quadratic majorization scheme. 

<h4>2.3.2 Higher Order</h4>

Most majorization algorithms discussed so far have a linear convergence rate, because `$\mathcal{D}f^2(x)$` is strictly smaller, in the Loewner sense, than `$\mathcal{D}_{11}g(x,x)$`. If we can find majorization schemes `$g$` with the same second order derivatives as the objective function `$f$`, then we will have a superlinear convergence rate.

Taylor's theorem, with the Lagrange remainder, tells us that for three-times differentiable functions

<div>
$$f(x)=f(y)+(x-y)'\mathcal{D}f(y)+\frac12 (x-y)'\mathcal{D}^2f(y)(x-y)+\frac16 \mathcal{D}^3f(\xi)\{(x-y)^3\},$$
</div>

with apologies for the notation. Here again `$\xi=\lambda x+(1-\lambda)y$` for some `$0\leq\lambda\leq 1$`. 

We get a 
majorization scheme by bounding the cubic term `$\mathcal{D}^3f(\xi)\{(x-y)^3\}.$` This can be done in various ways,
but most of them lead to majorization schemes that are difficult to minimize.

One of the more promising ones uses a bound of the form

<div>
$$\mathcal{D}^3f(\xi)\{(x-y)^3\}\leq\frac13 K\|x-y\|^3,$$
</div>

with `$\|x-y\|=\sqrt{(x-y)'(x-y)}$`.

This leads to minimization of the majorization scheme

<div>
$$g(x,y)=f(y)+(x-y)'\mathcal{D}f(y)+\frac12 (x-y)'\mathcal{D}^2f(y)(x-y)+\frac12 K\delta(x-y)'(x-y),$$
</div>

on the condition that `$\delta=\|x-y\|$`. The solution is a *regularized Newton step* of the form

<div>
$$x=y-\left[\mathcal{D}^2f(y)+K\delta I\right]^{-1}\mathcal{D}f(y),$$
</div> 

where `$\delta$` solves the single-variable *secular equation*

<div>
$$\delta^2=\mathcal{D}f(y)'\left[\mathcal{D}^2f(y)+K\delta I\right]^{-2}\mathcal{D}f(y).$$
</div> 

The secular equation can be solved efficiently, starting from the eigen-decomposition of `$\mathcal{D}^2f(y)$`.
Suppose `$L\Lambda L'$` is one such eigen-decomposition, and define `$g:=L'\mathcal{D}f(y)$`. Then we must solve

<div>
$$\delta^2=\sum_{i=1}^n \frac{g_i^2}{(\lambda_i+K\delta)^2}.$$
</div>

We again use logistic regression as an example. For the negative log-likelihood

<div>
$$\mathcal{D}^3f(x)=\sum_{i=1}^nn_i\pi_i(x)(1-\pi_i(x))(1-2\pi_i(x))\ z_i\otimes z_i\otimes z_i.$$
</div>

Now `$|\pi_i(x)(1-\pi_i(x))(1-2\pi_i(x))|\leq \frac{1}{18}\sqrt{3}$` so that

<div>
$$\mathcal{D}^3f(\xi)\{(x-y)^3\}\leq\frac{1}{18}\sqrt{3}\sum_{i=1}^nn_i|z_i'(x-y)|^3\leq\frac{1}{18}\sqrt{3}\sum_{i=1}^nn_i\|z_i\|^3\|x-y\|^3.$$
</div>

Thus

<div>
  $$K=\frac{1}{6}\sqrt{3}\sum_{i=1}^nn_i\|z_i\|^3.$$
</div>

The bound is crude, so it may take some iterations before superlinear convergence takes over.

<script type="text/javascript"
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  tex2jax: {
    inlineMath: [['$','$'], ['\$','\$`']],
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
MathJax.Hub.Config({
  CommonHTML: {
    scale: 110
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
