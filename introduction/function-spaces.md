---
exports:
  - format: pdf
    template: plain_latex
    output: exports/function-spaces.pdf
    id: introduction-function-spaces-pdf
downloads:
  - id: introduction-function-spaces-pdf
    title: Download PDF
---

# Function Spaces and Their Norms

## Learning Goals

1. What is a Banach space?
2. The spaces of continuous, differentiable and integrable functions.
3. What do $L^p$ norms measure? Intuition via bump functions.
4. The Rainbow of function spaces.


## Banach Spaces

````{prf:definition} Banach Space
:label: def-banach

A Banach space $(X, \|\cdot\|_X)$ is a complete normed vector space.
````

```{prf:example} Basic Banach Space
:label: ex-rn-banach

$\mathbb{R}^n$ is a Banach space with any p-norm i.e.
$\|x\|_p = \left( \sum_{i=1}^{n}|x_i|^p \right)^{1/p}$
```


## Spaces of Continuous and Differentiable Functions

```{prf:definition} $C^0$ — Continuous Functions
:label: def-c0

Let $\Omega \subset \mathbb{R}^n$ be open. The space of continuous functions on $\overline{\Omega}$ is

$$
C^0(\overline{\Omega}) = C(\overline{\Omega})
= \{ f : \overline{\Omega} \to \mathbb{R} : f \text{ is continuous} \}
$$

equipped with the **sup-norm** (or uniform norm)

$$
\|f\|_\infty = \sup_{x \in \overline{\Omega}} |f(x)|.
$$

When $\overline{\Omega}$ is compact, every continuous function is bounded and attains its supremum, so
$\|f\|_\infty < \infty$ for all $f \in C(\overline{\Omega})$.
```

```{prf:definition} $C^k$ — $k$-times Continuously Differentiable Functions
:label: def-ck

For $k \geq 1$, define

$$
C^k(\overline{\Omega}) = \{ f \in C(\overline{\Omega}) :
D^\alpha f \in C(\overline{\Omega}) \text{ for all } |\alpha| \leq k \}
$$

where $\alpha$ is a multi-index and $D^\alpha f$ denotes the corresponding partial derivative. This
space is equipped with the **$C^k$ norm**

$$
\|f\|_{C^k} = \sum_{|\alpha| \leq k} \|D^\alpha f\|_\infty
= \|f\|_\infty + \sum_{|\alpha|=1} \|D^\alpha f\|_\infty + \cdots
+ \sum_{|\alpha|=k} \|D^\alpha f\|_\infty.
$$
```

```{prf:definition} $C^\infty$ — Smooth Functions
:label: def-cinfty

The space of smooth (infinitely differentiable) functions is

$$
C^\infty(\overline{\Omega}) = \bigcap_{k=0}^{\infty} C^k(\overline{\Omega}).
$$

This space does not carry a single norm but is topologized by the family of $C^k$ seminorms: a
sequence $f_n \to f$ in $C^\infty$ if and only if $\|f_n - f\|_{C^k} \to 0$ for every $k$.
```

::::{dropdown} $C^\infty$ is not a Banach space — it is a Fréchet space

$C^\infty(\overline{\Omega})$ is **not** a Banach space because no single norm can capture its
topology. It is instead a **Fréchet space**: a complete, metrizable, locally convex topological vector
space whose topology is defined by a *countable* family of seminorms (here, $\|\cdot\|_{C^k}$ for
$k = 0, 1, 2, \dots$).

**Why can't a single norm work?** For any fixed $k$, there exist sequences in $C^\infty$ that
converge in $C^k$ but diverge in $C^{k+1}$. For example, on $[0,1]$:

$$
f_n(x) = \frac{\sin(n x)}{n}
$$

converges to $0$ in $C^0$ ($\|f_n\|_\infty = 1/n \to 0$), but $f_n'(x) = \cos(nx)$ does not converge
at all — the $C^1$ norms satisfy $\|f_n\|_{C^1} \geq 1$ for all $n$. No matter which $C^k$ norm you
pick, there is always a "higher" derivative direction that it fails to control.

A Banach space norm would have to simultaneously control all derivatives, but controlling the $k$-th
derivative imposes constraints that are strictly independent of controlling the $(k-1)$-th. Formally,
$C^\infty$ is not *normable*: by Kolmogorov's criterion, a locally convex space admits a norm if and
only if it has a bounded neighborhood of zero, and in $C^\infty$ every neighborhood of zero contains
functions with arbitrarily large $k$-th derivatives for sufficiently large $k$.

Despite not being Banach, $C^\infty$ is **complete** in its Fréchet topology (a Cauchy sequence in
every $C^k$ norm converges in every $C^k$ norm), and much of the Banach space theory
— including versions of the Open Mapping Theorem and Closed Graph Theorem — extends to
Fréchet spaces.

::::

### What Do $C^k$ Norms Measure?

The $C^k$ norm controls the function **and** its first $k$ derivatives uniformly. This has a concrete
geometric meaning:

- **$\|f\|_{C^0} = \|f\|_\infty$** controls the **height**: two functions are $C^0$-close if their
  graphs are uniformly close.
- **$\|f\|_{C^1} = \|f\|_\infty + \|f'\|_\infty$** additionally controls the **slope**: two functions
  are $C^1$-close if their graphs are close *and* their tangent lines are close at every point.
- **$\|f\|_{C^k}$** controls curvature, jerk, and higher-order shape information. Closeness in $C^k$
  means the functions "look the same" up to $k$-th order magnification.

The key point: **higher-order $C^k$ norms are strictly stronger**. A sequence can converge in $C^0$
(graphs converge) without converging in $C^1$ (slopes may oscillate wildly).

```{prf:example} $C^1$ with the sup-norm is incomplete
:label: ex-c1-incomplete

The space $C^1([0,1])$ equipped with the **wrong** norm $\|\cdot\|_\infty$ (instead of
$\|\cdot\|_{C^1}$) is **not** a Banach space.

Consider the sequence $f_n(x) = \sqrt{x + 1/n}$ on $[0,1]$. Each $f_n$ is $C^1$, and $f_n \to
f(x) = \sqrt{x}$ uniformly. But $f(x) = \sqrt{x}$ is not differentiable at $x = 0$, so
$f \notin C^1([0,1])$.

The sup-norm cannot detect that the derivatives $f_n'(x) = \frac{1}{2\sqrt{x + 1/n}}$ are blowing up
near $x = 0$. The $C^1$ norm would catch this: $\|f_n\|_{C^1} \to \infty$, so the sequence is not
Cauchy in the $C^1$ norm.

This is a concrete instance of a general principle: **a function space is only complete in a norm
strong enough to detect all the structure the space requires**. The sup-norm is too weak for $C^1$—it
measures height but not slope, so Cauchy sequences can converge to functions that are continuous but
not differentiable.
```

```{prf:proposition} $C^k(\overline{\Omega})$ is a Banach space
:label: prop-ck-banach

For $\overline{\Omega}$ compact and $k \geq 0$, the space $(C^k(\overline{\Omega}), \|\cdot\|_{C^k})$
is a Banach space.
```

```{dropdown} **Proof sketch:**
Let $\{f_n\}$ be Cauchy in $C^k$. Then for each $|\alpha| \leq k$, the sequence $\{D^\alpha f_n\}$ is
Cauchy in $C^0$ (sup-norm). Since $(C^0, \|\cdot\|_\infty)$ is complete, each $D^\alpha f_n$
converges uniformly to some continuous function $g_\alpha$. A standard argument (integrating and
differentiating under the limit) shows $g_\alpha = D^\alpha g_0$, so $g_0 \in C^k$ and
$f_n \to g_0$ in $C^k$.
```

## Spaces of Integrable Functions

```{prf:definition} $L^p$ Spaces
:label: def-lp-spaces

For $1 \leq p < \infty$ we define the spaces of $p$-integrable functions

$$L^p(\Omega) = \left\{f : \Omega \to \mathbb{R} : \|f\|_p = \left( \int_{\Omega} |f(x)|^p \, d\mu \right)^{1/p} < \infty \right\} \Big/ \sim$$

where $f \sim g$ if $f = g$ **almost everywhere** (i.e., $\mu(\{x : f(x) \neq g(x)\}) = 0$).

For $p = \infty$ we define

$$L^\infty(\Omega) = \left\{f : \Omega \to \mathbb{R} : \|f\|_\infty = \operatorname{ess\,sup}_{x \in \Omega} |f(x)| < \infty \right\} \Big/ \sim$$
```

::::{dropdown} Why equivalence classes?

Strictly speaking, elements of $L^p$ are not functions but **equivalence classes** of functions that
agree almost everywhere. This quotient is essential: without it, $\|\cdot\|_p$ is only a **seminorm**,
not a norm. The problem is that $\|f\|_p = 0$ does not imply $f = 0$ pointwise—only $f = 0$ a.e.
For instance, the function that equals $1$ at a single point and $0$ elsewhere has $L^p$ norm zero
but is not the zero function. Passing to equivalence classes identifies all such functions with the
zero class, making $\|f\|_p = 0 \implies f = 0$ in $L^p$.

This is a fundamental difference from $C^k$ spaces, where functions are determined by their pointwise
values and the sup-norm is a genuine norm without any quotienting.

::::

## What Do $L^p$ Norms Measure?

Different norms capture different features of a function. To build intuition, consider a smooth bump function $\phi \in \mathcal{C}^\infty_c(\mathbb{R})$ with $\phi \geq 0$, $\operatorname{supp}(\phi) \subset [-1, 1]$, and $\|\phi\|_\infty = 1$.

We construct two families of functions that independently control **height** and **width**.

**Scaling the height.** Define $f_A(x) = A\,\phi(x)$ for $A > 0$. This rescales the amplitude without changing the support. Then:

$$\|f_A\|_\infty = A, \qquad \|f_A\|_1 = A\|\phi\|_1, \qquad \|f_A\|_p = A\|\phi\|_p.$$

All norms see the height equally — no surprise, since we are simply rescaling the function values.

**Scaling the width.** Define $g_R(x) = \phi(x/R)$ for $R > 0$. This stretches the support to $[-R, R]$ without changing the peak value. Then:

$$\|g_R\|_\infty = \|\phi\|_\infty = 1$$

is **independent of $R$** — the $L^\infty$ norm is completely insensitive to how wide the function is. On the other hand, by a change of variables $y = x/R$:

$$\|g_R\|_p^p = \int |g_R(x)|^p \, dx = R \int |\phi(y)|^p \, dy = R\,\|\phi\|_p^p$$

so that $\|g_R\|_p = R^{1/p}\|\phi\|_p$, which **grows** as we widen the support.

```{prf:remark} Interpretation of $L^p$ Norms
:label: rem-lp-interpretation

This analysis reveals a fundamental distinction:

- **$L^\infty$** measures only the **height** (peak value) of a function. It is completely insensitive to the width of the support.
- **$L^1$** measures the **total mass** — it averages the function over the domain, so both height and width contribute equally.
- **$L^p$** for $1 < p < \infty$ **interpolates** between these extremes: larger $p$ gives more weight to peak values and less to the spread.

This is why $L^\infty$ convergence (uniform convergence) is a much stronger requirement than $L^1$ convergence: a sequence of tall, narrow spikes can have $L^1$ norm tending to zero while the $L^\infty$ norm remains constant.
```


## $L^p$ is a Banach Space

````{prf:theorem} $L^p$ is a Banach Space
:label: thm-lp-banach

$L^p$ is a Banach space.

```{dropdown} **Proof:**

We must show that every Cauchy sequence in $L^p$ converges. Let $\{f_n\}$ be a Cauchy sequence in $L^p$ i.e. $\forall \varepsilon > 0$ $\exists N :$ $\|f_n - f_m\| < \varepsilon$ $\forall n,m > N$.

Recall that we can extract a subsequence from a Cauchy sequence (I believe this is often called a diagonal Cantor argument?) by selecting an increasing sequence $n_j$ such that
$\|f_{n_{k+1}} - f_{n_k}\| < 2^{-k},\ k = 1, 2, \dots$

Define
$G_k := \sum_{k=1}^{K} |f_{n_{k+1}} - f_{n_k}|$

and $G = \lim_k G_k$. By Minkowski's inequality we have
$\|G_k\|_p \leq \sum_{k=1}^{K} \|f_{n_{k+1}} - f_{n_k}\| \leq 1$

for all $k$. Since $G_k$ is an increasing sequence we apply the Monotone convergence theorem
$\int G^p d\mu = \int \lim_k G_k^p d\mu = \lim_k \int G_k^p d\mu \leq 1$

This implies that $G \in L^p$ and thus $G(x) < \infty$ almost everywhere.
Define
$f(x) = f_{n_1} + \sum_{k=1}^{\infty} f_{n_{k+1}} - f_{n_k}$

Note that this is a telescoping sum so we have that $f_{n_k} \to f(x)$ almost everywhere. We also have
$\|f\|_p \leq \|f_{n_1}\|_p + \|G\|_p < \infty$

Thus $f \in L^p$.
Finally, we apply Fatou's lemma (to show that $f_n \to f$ in $L^p$)
$\int \|f - f_n\|^p d\mu = \int \lim_{k \to \infty} \|f_{n_k} - f_n\|^p d \mu \leq \liminf_{k \to \infty} \int \|f_{n_k} - f_n\|^p d \mu \leq \varepsilon^p$

when $n_k > N$. Thus we have that $\|f - f_n\| \to 0$.
```

````


## The Rainbow of Function Spaces

```{prf:remark} The Rainbow of Function Spaces
:label: rem-rainbow

A key result from this lecture is the "rainbow" of function spaces. The spaces of continuous and differentiable functions naturally are nested. Similarly, the spaces of integrable functions are nested by Hölder's inequality for bounded domains.

In particular, spaces of integrable functions are only nestable when the measure of the domain is finite or the counting measure (in this case the role of $p$ and $q$ reverse). Thus crucially spaces of integrable functions with unbounded domains are **not** nested.
```
