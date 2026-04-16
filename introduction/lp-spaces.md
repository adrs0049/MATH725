---
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/lp-spaces.pdf
    id: introduction-lp-spaces-pdf
downloads:
  - id: introduction-lp-spaces-pdf
    title: Download PDF
---

# Spaces of Integrable Functions

## Learning Goals

1. The spaces of integrable functions.
2. What do $L^p$ norms measure? Intuition via bump functions.
3. The Rainbow of function spaces.


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
