---
exports:
  - format: pdf
    template: plain_latex
    output: exports/approximation.pdf
    id: introduction-approximation-pdf
downloads:
  - id: introduction-approximation-pdf
    title: Download PDF
---

# Density and Approximation

A central theme in functional analysis is **approximation**: given a function in some large space, can we approximate it arbitrarily well by functions from a nicer, more structured class? This question is formalized through the notions of density and separability.

## Dense Subsets

```{prf:definition} Dense Subset
:label: def-dense

A subset $Y\subset X$ is dense in $X$ if $\bar{Y} = X$. Equivalently, given $x\in X$, $\forall \varepsilon > 0$ $\exists y \in Y$ such that $\|x - y\| < \varepsilon$.
```

```{prf:example} Rationals in Reals
:label: ex-q-dense-r

$\bar{\mathbb{Q}} = \mathbb{R}$. Let $r \in \mathbb{R}$ and $\varepsilon > 0$ then there is $n$ such that $\frac{1}{n} < \varepsilon$. Define $q_n = \frac{\lfloor nr\rfloor}{n}$ which implies that
$\|r - \frac{nr}{n}\| < \frac{1}{n} < \varepsilon$

In other words we can approximate any real number $r$ arbitrarily well by elements in the rationals e.g. the rationals are dense in the reals. This property of the rationals is crucially important for finite arithmetic approximations of the reals on computers.
```

```{prf:example} Weierstrass Theorem
:label: ex-weierstrass

Let $f \in \mathcal{C}^0([-1, 1])$ and let $\varepsilon > 0$ then there exists a polynomial $p$ such that $\|f - p\|_{\infty} < \varepsilon$.
```


## Separability

```{prf:definition} Separable Space
:label: def-separable

A Banach space which contains a dense **countable** subset is called separable.
```

```{prf:example} Separability of Real Numbers
:label: ex-r-separable

Since the rationals are countable and dense in $\mathbb{R}$, thus $\mathbb{R}$ is separable.
```

```{prf:example} Separability of Continuous Functions
:label: ex-c0-separable

$\mathcal{C}^0([-1, 1])$ has the dense subset
$\{ ax^n : a \in \mathbb{Q},\ n \in \mathbb{N} \cup \{ 0 \} \}$

This set is countable and dense in $\mathcal{C}^0([-1, 1])$: we can approximate any continuous function using a polynomial having rational coefficients. Thus $\mathcal{C}^0([-1, 1])$ is a separable Banach space.
```

```{prf:example} Separability of Square Integrable Functions
:label: ex-l2-separable

The space of square integrable functions $L^2([-1, 1])$ has basis set
$\{ 1,\ \cos(nx),\ \sin(nx)\}$

which is countable and hence it is a separable space.
```

```{prf:example} Non-separability of L-infinity
:label: ex-linf-not-separable

$L^\infty([-1, 1])$ is not separable (see homework).
```


## Mollification

The key technique for approximating rough functions by smooth ones is **mollification** — convolution with a smooth bump function that averages a function over a small neighborhood.

```{prf:theorem} Mollifiers Theorem
:label: thm-mollifiers

Given $f \in \mathcal{C}^0_c(\Omega)$, for each $\varepsilon > 0$ $\exists \phi \in \mathcal{C}^\infty_c(\Omega)$ such that
$\|f - \phi\|_{\infty} < \varepsilon$
```

This is a powerful result: it tells us that any continuous function with compact support can be uniformly approximated by smooth, compactly supported functions. The idea is to convolve $f$ with a smooth bump (a mollifier) at a sufficiently small scale.


## Density of Smooth Functions in $L^p$

Mollification is the engine behind the fundamental density results for $L^p$ spaces.

````{prf:theorem} Density of $\mathcal{C}^0$ in $L^p$
:label: thm-c0-dense-lp

Let $\Omega$ be bounded, then $\mathcal{C}^0(\Omega)$ is dense in $L^p(\Omega)$ i.e.

$$L^p(\Omega) = \overline{\mathcal{C}^0_c(\Omega)}$$

where the closure is with respect to the $p$-norm, and $L^p$ is separable.

```{dropdown} **Proof:**

The key to the proof is to recall that any measurable function can be approximated using simple functions. Recall that we say a function is simple if
$s_n = \sum_{i = 1}^{n} c_j \chi_{I_j}(x)$

where $\chi_{I_j}$ is the indicator function of a set, recall that from the construction of the Lebesgue integral these sets can be complicated (i.e. contain several disjointed pieces). Then given any measurable function $f(x)$ we can find a sequence of increasing simple functions (i.e. $s_1(x) \leq s_2(x) \leq \dots \leq f(x)$) such that $s_n(x) \to f(x)$ pointwise for almost every $x$ i.e. $|s_n - f| < \varepsilon$.

We have that $|s_n - f|^p \leq 2|f|^p \in L^1$ and the Lebesgue dominated convergence theorem implies that
$\lim_{n\to\infty} \int |s_n - f|^p d\mu = \int \lim_{n\to\infty} |s_n - f|^p d\mu \leq C \varepsilon$

Thus we have that $\|s_n - f\|_p \to 0$.
Finally note that each simple function is continuous and we can pick the weights to be rational, and for the final step mollify each of the characteristic functions.
```
````

Combining with the mollifiers theorem, we obtain the density of smooth functions.

```{prf:corollary} Density of $\mathcal{C}^\infty_c$ in $L^p$
:label: cor-cinfty-dense-lp

Let $\Omega$ be bounded. Then $\mathcal{C}^\infty_c(\Omega)$ is dense in $L^p(\Omega)$:

$$L^p(\Omega) = \overline{\mathcal{C}^\infty_c(\Omega)}$$
```


## Approximation Beyond Polynomials

The classical approximation results above — Weierstrass, mollification, density of $\mathcal{C}^\infty$ in $L^p$ — all share a common structure: they identify a "nice" class of functions (polynomials, smooth functions) that can approximate arbitrary elements of a larger space.

```{prf:remark} Toward Neural Network Approximation
:label: rem-nn-approximation

A natural question is: what other classes of functions are dense in common function spaces? It turns out that **neural networks** provide a modern and remarkably powerful answer. The Universal Approximation Theorem (Cybenko, 1989; Hornik, 1991) shows that single-hidden-layer neural networks with sufficiently many neurons are dense in $\mathcal{C}^0(K)$ for any compact $K$, and consequently in $L^p$.

From the functional-analytic viewpoint, this is a density result: the set of functions representable by a neural network architecture is dense in the spaces we care about. The proof, which we will see later in the course, is a beautiful application of the Hahn-Banach theorem — one of the central results in duality theory. We will develop this connection in detail in the chapter on Neural Network Connections.
```
