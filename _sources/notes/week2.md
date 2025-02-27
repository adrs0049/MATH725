# The Basics
*February 3, 2024*
*Weekly Course Outline*

**Note**, this week did not have a Tuesday lecture due to delayed term start.

## Learning Goals

The goals of these few lectures is to review a few core ideas, and set the stage of classic function spaces we will use to develop the theory.

1. The Basics of Functional Analysis.
2. What is a Banach Space?
3. Density, separability and compactness.

---

:::{prf:definition} Banach Space
:class: definition
:label: def-banach

A Banach space $(X, \|\cdot\|_X)$ is a complete normed vector space.
:::

:::{prf:example} Basic Banach Space
:class: example
:label: ex-rn-banach

$\mathbb{R}^n$ is a Banach space with any p-norm i.e.
$$\|x\|_p = \left( \sum_{i=1}^{n}|x_i|^p \right)^{1/p}$$
:::

---

We need the following basic topological notions.

:::{prf:definition} Dense Subset
:label: def-dense
A subset $Y\subset X$ is dense in $X$ if $\bar{Y} = X$. Equivalently, given $x\in X$ $\forall \varepsilon > 0$ $\exists y \in Y$ such that $\|x - y\| < \varepsilon$.
:::

:::{prf:example} Rationals in Reals
:label: ex-q-dense-r
$\bar{\mathbb{Q}} = \mathbb{R}$. Let $r \in \mathbb{R}$ and $\varepsilon > 0$ then there is $n$ such that $\frac{1}{n} < \varepsilon$. Define $q_n = \frac{\lfloor nr\rfloor}{n}$ which implies that
$$\|r - \frac{nr}{n}\| < \frac{1}{n} < \varepsilon$$

In other words we can approximate any real number $r$ arbitrarily well by elements in the rationals e.g. the rationals are dense in the reals. This property of the rationals is crucially important for finite arithmetic approximations of the reals on computers.
:::

:::{prf:example} Weierstrass Theorem
:label: ex-weierstrass
Let $f \in \mathcal{C}^0([-1, 1])$ and let $\varepsilon > 0$ then there exists a polynomial $p$ such that $\|f - p\|_{\infty} < \varepsilon$.
:::

:::{prf:definition} Separable Space
:label: def-separable
A Banach space which contains a dense **countable** subset is called separable.
:::

:::{prf:example} Separability of Real Numbers
:label: ex-r-separable
Since the rationals are countable and dense in $\mathbb{R}$, thus $\mathbb{R}$ is separable.
:::

:::{prf:example} Separability of Continuous Functions
:label: ex-c0-separable
$\mathcal{C}^0([-1, 1])$ define the basis set
$$\{ ax^n : a \in \mathbb{Q},\ n \in \mathbb{N} \cup \{ 0 \} \}$$

this set is countable and dense in $\mathcal{C}^0([-1, 1])$ in other words we can approximate any continuous function using a polynomial having rational coefficients. Thus we have a countable Banach space.
:::

:::{prf:example} Separability of Square Integrable Functions
:label: ex-l2-separable
The space of square integrable functions $L^2([-1, 1])$ has basis set
$$\{ 1,\ \cos(nx),\ \sin(nx)\}$$

which is countable and hence it is a separable space.
:::

:::{prf:example} Non-separability of L-infinity
:label: ex-linf-not-separable
$L^\infty([-1, 1])$ is not separable (see homework).
:::

:::{prf:definition} Compact Set
:label: def-compact
A subset $E \subset X$ is compact if either:
1. each open cover contains a finite subcover.
2. each sequence $\{x_n\} \subset E$ contains a convergent subsequence.
:::

:::{prf:example} Compactness of Unit Ball in R^n
:label: ex-unit-ball-compact
The closed unit ball
$$B_1(0) = \{x \in \mathbb{R}^n : \|x\|_p \leq 1\}$$

is compact by Heine-Borel. Equivalently, we can take any sequence $\{x_n\} \subset B_1(0)$. Since that sequence is bounded Bolzano-Weierstrass implies that it has a convergence subsequence.
:::

:::{prf:remark} Compactness in Infinite Dimensions
:label: rem-compact-infinite
While any closed and bounded subset of $\mathbb{R}^n$ is compact, this dramatically changes in infinite dimensions where the closed unit ball is not compact (we see this at the end of this week). For this reason, compactness results play a crucial role in functional analysis.
:::

:::{prf:definition} Equivalent Norms
:label: def-equiv-norms
Two norms $\|x\|^1$ and $\|x\|^2$ are equivalent if there exists $a, b > 0$ such that
$$a \|x\|^1 \leq \|x\|^2 \leq b \|x\|^1\quad \forall x \in X$$
:::

Note that the previous definition calls two norms equivalent when they induce the same underlying topology on $X$. In other words, they generate the same open sets or intuitively induce the same notion of two elements being close.

:::{prf:theorem} Equivalence of Norms in R^n
:label: thm-rn-norms-equiv
In $\mathbb{R}^n$ all norms are equivalent.
:::

:::{prf:proof}
This is merely a sketch of a proof. They key idea is that in $\mathbb{R}^n$ all the unit balls can be scaled so that they fit into each other. Allowing us to show that the open sets in $(\mathbb{R}^n, \|x\|_p)$ are the same as in $(\mathbb{R}^n, \|x\|_q)$.
:::

## Lesson: Thursday

### Learning Goals

Define some typical function spaces that are central to the theory.

1. The spaces of continuous, differentiable and integral functions.
2. Density, Separability in $L^p$ spaces e.g. approximation of functions by simple functions.
3. The Rainbow of function spaces.

---

For the definitions of the spaces of continuous, continuously differentiable and Hoelder continuous functions see the class textbook.

---

:::{prf:definition} L^p Spaces
:label: def-lp-spaces
For $1 \leq p < \infty$ we define the spaces of integrable functions
$$L^p(\Omega) = \{f : \Omega \mapsto \mathbb{R} : \|f\|_p = \left( \int_{\Omega} |f(x)|^p d\mu \right)^{1/p} < \infty \}$$
:::

:::{prf:theorem} Mollifiers Theorem
:label: thm-mollifiers
Given $f \in \mathcal{C}^0_c(\Omega)$, for each $\varepsilon > 0$ $\exists \phi \in \mathcal{C}^\infty_c(\Omega)$ such that
$$\|f - \phi\|_{\infty} < \varepsilon$$
:::

:::{prf:theorem} Density of C^0 in L^p
:label: thm-c0-dense-lp
Let $\Omega$ be bounded, then $\mathcal{C}^0(\Omega)$ is dense in $L^p(\Omega)$ i.e.
$$L^p(\Omega) = \overline{\mathcal{C}^0_c(\Omega)}$$

where the closure is wrt. to the p-norm, and $L^p$ is separable.
:::

:::{prf:proof}
The key to the proof is to recall that any measurable function can be approximated using simple functions. Recall that we say a function is simple if
$$s_n = \sum_{i = 1}^{n} c_j \chi_{I_j}(x)$$

where $\chi_{I_j}$ is the indicator function of a set, recall that from the construction of the Lebesque integral these sets can be complicated (i.e. contain several disjointed pieces). Then given any measurable function $f(x)$ we can find a sequence of increasing simple functions (i.e. $s_1(x) \leq s_2(x) \leq \dots \leq f(x)$) such that $s_n(x) \to f(x)$ pointwise for almost every $x$ i.e. $|s_n - f| < \varepsilon$.

We have that $|s_n - f|^p \leq 2|f|^p \in L^1$ and the Lebesgue dominated convergence theorem implies that
$$\lim_{n\to\infty} \int |s_n - f|^p d\mu = \int \lim_{n\to\infty} |s_n - f|^p d\mu \leq C \varepsilon$$

Thus we have that $\|s_n - f\|_p \to 0$.
Finally note that each simple function is continuous and we can pick the weights to be rational, and for the final step mollify each of the characteristic functions.
:::

:::{prf:theorem} L^p is a Banach Space
:label: thm-lp-banach
$L^p$ is a Banach space.
:::

:::{prf:proof}
We must show that every Cauchy sequence in $L^p$ converges. Let $\{f_n\}$ be a Cauchy sequence in $L^p$ i.e. $\forall \varepsilon > 0$ $\exists N :$ $\|f_n - f_m\| < \varepsilon$ $\forall n,m > N$.

Recall that we can extract a subsequence from a Cauchy sequence (I believe this is often called a diagonal Cantor argument?) by selecting an increasing sequence $n_j$ such that
$$\|f_{n_{k+1}} - f_{n_k}\| < 2^{-k},\ k = 1, 2, \dots$$

Define
$$G_k := \sum_{k=1}^{K} |f_{n_{k+1}} - f_{n_k}|$$

and $G = \lim_k G_k$. By Minkowski's inequality we have
$$\|G_k\|_p \leq \sum_{k=1}^{K} \|f_{n_{k+1}} - f_{n_k}\| \leq 1$$

for all $k$. Since $G_k$ is an increasing sequence we apply the Monotone convergence theorem
$$\int G^p d\mu = \int \lim_k G_k^p d\mu = \lim_k \int G_k^p d\mu \leq 1$$

This implies that $G \in L^p$ and thus $G(x) < \infty$ almost everywhere.
Define
$$f(x) = f_{n_1} + \sum_{k=1}^{\infty} f_{n_{k+1}} - f_{n_k}$$

Note that this is a telescoping sum so we have that $f_{n_k} \to f(x)$ almost everywhere. We also have
$$\|f\|_p \leq \|f_{n_1}\|_p + \|G\|_p < \infty$$

Thus $f \in L^p$.
Finally, we apply Fatou's lemma (to show that $f_n \to f$ in $L^p$)
$$\int \|f - f_n\|^p d\mu = \int \lim_{k \to \infty} \|f_{n_k} - f_n\|^p d \mu \leq \liminf_{k \to \infty} \int \|f_{n_k} - f_n\|^p d \mu \leq \varepsilon^p$$

when $n_k > N$. Thus we have that $\|f - f_n\| \to 0$.
:::

---

:::{prf:remark} The Rainbow of Function Spaces
:label: rem-rainbow
A key result from this lecture is the "rainbow" of function spaces. The spaces of continuous and differentiable functions naturally are nested. Similarly, the spaces of integrable functions are nested by Hoelder's inequality for bounded domains.

In particular, spaces of integrable functions are only nestable when the measure of the domain is finite or the counting measure (in this case the role of $p$ and $q$ reverse). Thus crucially spaces of integrable functions with unbounded domains are **not** nested.
:::

---

