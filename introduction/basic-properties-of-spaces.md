---
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/compactness.pdf
    id: introduction-compactness-pdf
downloads:
  - id: introduction-compactness-pdf
    title: Download PDF
---

# Compactness

Almost every existence argument in analysis follows the same three-step template:

1. **Construct an approximate sequence** of "almost-solutions" (minimizing sequences, Galerkin
   approximations, Euler polygonal approximations, maximizers of a Rayleigh quotient, etc.).
2. **Extract a convergent subsequence.** This is where compactness enters.
3. **Pass to the limit.** Show the limit actually solves the original problem.

In finite dimensions step 2 is free: Bolzano-Weierstrass guarantees that every bounded sequence in
$\mathbb{R}^n$ has a convergent subsequence. This is why eigenvalue decompositions, the SVD, the
direct method of the calculus of variations, and Peano's ODE existence theorem all "just work" in
$\mathbb{R}^n$. Each reduces to building an approximate sequence on a compact set and extracting a
convergent subsequence. In infinite dimensions, closed bounded sets are no longer compact, and step
2 fails without additional structure.

```{prf:definition} Compact, precompact, and totally bounded sets
:label: def-compact-precompact

Let $(M, d)$ be a metric space and $A \subset M$.

1. $A$ is **compact** if every open cover of $A$ has a finite subcover, or equivalently, if every
   sequence in $A$ has a subsequence converging to a point in $A$.
2. $A$ is **precompact** (or **relatively compact**) if its closure $\overline{A}$ is compact, or
   equivalently, if every sequence in $A$ has a subsequence that is Cauchy.
3. $A$ is **totally bounded** if for every $\varepsilon > 0$, $A$ can be covered by finitely many
   balls of radius $\varepsilon$.
```

The key equivalence is:

> **$A$ is compact $\iff$ $A$ is complete and totally bounded.**

In a complete metric space (such as a Banach space), precompactness and total boundedness coincide:
$A$ is precompact if and only if it is totally bounded.

**Why both conditions are needed.**
- *Total boundedness without completeness fails.* The open interval $(0,1)$ is totally bounded in
  $\mathbb{R}$, but the sequence $1/n$ converges to $0 \notin (0,1)$. The limit escapes through a
  "hole."
- *Completeness without total boundedness fails.* The unit ball of $\ell^2$ is complete, but the
  orthonormal sequence $(e_n)$ has all elements distance $\sqrt{2}$ apart, so no finite
  $\varepsilon$-cover works for $\varepsilon < \sqrt{2}/2$. There are "too many directions."

Total boundedness is the condition that makes a set **approximately finite-dimensional**: at every
resolution $\varepsilon$, the set is indistinguishable from a finite set. Completeness then ensures
that Cauchy subsequences (built by the pigeonhole principle at finer and finer scales) actually
converge.

In finite dimensions, compactness is characterized by the Heine-Borel theorem: a set is compact if and only if it is closed and bounded.

```{prf:example} Compactness of Unit Ball in $\mathbb{R}^n$
:label: ex-unit-ball-compact

The closed unit ball
$B_1(0) = \{x \in \mathbb{R}^n : \|x\|_p \leq 1\}$

is compact by Heine-Borel. Equivalently, we can take any sequence $\{x_n\} \subset B_1(0)$. Since that sequence is bounded Bolzano-Weierstrass implies that it has a convergent subsequence.
```

This picture changes dramatically in infinite dimensions.

````{prf:example} The Unit Ball in $\ell^2$ is Not Compact
:label: ex-unit-ball-l2-not-compact

Consider the Hilbert space $\ell^2$ of square-summable sequences with the standard orthonormal basis $\{e_n\}_{n=1}^\infty$ where $e_n = (0, \ldots, 0, 1, 0, \ldots)$ has a $1$ in position $n$ and zeros elsewhere.

Each $e_n$ lies in the closed unit ball since $\|e_n\|_2 = 1$. However, for any $n \neq m$:

$$\|e_n - e_m\|_2 = \sqrt{\|e_n\|_2^2 + \|e_m\|_2^2} = \sqrt{2}$$

Every pair of distinct elements is at distance $\sqrt{2}$ apart. Therefore no subsequence of $\{e_n\}$ can be Cauchy, and hence no subsequence converges. The closed unit ball in $\ell^2$ is **not** compact.
````

```{prf:remark} Compactness in Infinite Dimensions
:label: rem-compact-infinite

The failure of the Heine-Borel theorem in infinite dimensions is one of the most important distinctions between finite- and infinite-dimensional analysis. Closed and bounded sets need not be compact, and establishing compactness requires additional structure (e.g. equicontinuity in the Arzelà-Ascoli theorem, or tightness in probability theory). For this reason, compactness arguments play a crucial and often delicate role throughout functional analysis.
```

```{prf:remark} Compact sets in infinite dimensions
:label: rem-compact-sets-inf-dim

Boundedness alone is not enough. The unit ball of $\ell^2$ is closed and bounded, yet the
orthonormal sequence $(e_n)$ has every pair distance $\sqrt{2}$ apart, so no subsequence can be
Cauchy. You need a constraint that suppresses this "too many directions" problem, i.e. you need
total boundedness ({prf:ref}`def-compact-precompact`).

A concrete and important example: the unit ball of $H^1(\Omega)$, viewed inside $L^2(\Omega)$, is
precompact (Rellich-Kondrachov). The reason is visible in Fourier space. An $H^1$ bound forces
$|\hat{u}(k)|^2 \leq C/(1 + |k|^2)$, so high-frequency modes are uniformly suppressed. For any
$\varepsilon > 0$, all the $L^2$ energy beyond a sufficiently large frequency $N$ is less than
$\varepsilon$, uniformly over the entire $H^1$ ball. The remaining low-frequency part lives in a
finite-dimensional space. This is total boundedness: the derivative bound kills oscillations that
would otherwise prevent clustering, and the bounded domain prevents mass from escaping to spatial
infinity.
```


