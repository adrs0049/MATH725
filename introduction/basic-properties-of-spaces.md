---
exports:
  - format: pdf
    template: plain_latex
    output: exports/basic-properties-of-spaces.pdf
    id: introduction-basic-properties-of-spaces-pdf
downloads:
  - id: introduction-basic-properties-of-spaces-pdf
    title: Download PDF
---

# Compactness and Topological Equivalence

We now turn to two fundamental topological properties of Banach spaces that distinguish finite-dimensional spaces from infinite-dimensional ones: compactness of bounded sets and equivalence of norms.


## Compactness

```{prf:definition} Compact Set
:label: def-compact

A subset $E \subset X$ is compact if either:
1. each open cover contains a finite subcover.
2. each sequence $\{x_n\} \subset E$ contains a convergent subsequence.
```

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


## Equivalence of Norms

```{prf:definition} Equivalent Norms
:label: def-equiv-norms

Two norms $\|x\|^1$ and $\|x\|^2$ are equivalent if there exists $a, b > 0$ such that
$a \|x\|^1 \leq \|x\|^2 \leq b \|x\|^1\quad \forall x \in X$
```

Note that the previous definition calls two norms equivalent when they induce the same underlying topology on $X$. In other words, they generate the same open sets or intuitively induce the same notion of two elements being close.

**Geometric intuition.** The condition $a\|x\|^1 \leq \|x\|^2 \leq b\|x\|^1$ says that the unit ball of one norm can be scaled to fit inside the unit ball of the other, and vice versa. In $\mathbb{R}^2$, for example, the $\ell^1$ ball (a diamond), the $\ell^2$ ball (a circle), and the $\ell^\infty$ ball (a square) all have different shapes — but each one can be scaled up or down to contain, or be contained in, any of the others. This mutual containment of balls is exactly what equivalent topologies means: the same sequences converge, the same sets are open, and the same functions are continuous.

```{prf:theorem} Equivalence of Norms in $\mathbb{R}^n$
:label: thm-rn-norms-equiv

In $\mathbb{R}^n$ all norms are equivalent.
```

```{prf:proof}

This is merely a sketch of a proof. The key idea is that in $\mathbb{R}^n$ all the unit balls can be scaled so that they fit into each other. Allowing us to show that the open sets in $(\mathbb{R}^n, \|x\|_p)$ are the same as in $(\mathbb{R}^n, \|x\|_q)$.
```

```{prf:remark} Failure in Infinite Dimensions
:label: rem-norms-not-equiv-infinite

This theorem fails in infinite dimensions. For instance, on $\mathcal{C}^0([0,1])$ the norms $\|\cdot\|_\infty$ and $\|\cdot\|_1$ are **not** equivalent: a sequence of functions can converge in $L^1$ without converging uniformly. The choice of norm — and hence the topology — matters fundamentally in infinite-dimensional analysis and determines which operators are bounded, which functionals are continuous, and which sequences converge.
```
