---
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/topological-equivalence.pdf
    id: introduction-topological-equivalence-pdf
downloads:
  - id: introduction-topological-equivalence-pdf
    title: Download PDF
---

# Topological Equivalence of Norms

A single vector space can carry many different norms. Two norms are *equivalent* when they induce
the same topology — the same open sets, the same convergent sequences, the same continuous
functions. In finite dimensions this never matters: all norms on $\mathbb{R}^n$ are equivalent. In
infinite dimensions it matters enormously, and the choice of norm determines which operators are
bounded and which sequences converge.

```{prf:definition} Equivalent Norms
:label: def-equiv-norms

Two norms $\|\cdot\|^1$ and $\|\cdot\|^2$ on a vector space $X$ are **equivalent** if there exist
constants $a, b > 0$ such that

$$a \|x\|^1 \leq \|x\|^2 \leq b \|x\|^1 \quad \forall x \in X.$$
```

Equivalent norms induce the same underlying topology on $X$: they generate the same open sets and
hence the same notion of "close."

**Geometric intuition.** The condition $a\|x\|^1 \leq \|x\|^2 \leq b\|x\|^1$ says the unit ball of
one norm can be scaled to sit inside the unit ball of the other, and vice versa. In $\mathbb{R}^2$
the $\ell^1$ ball (a diamond), the $\ell^2$ ball (a circle), and the $\ell^\infty$ ball (a square)
all have different shapes — yet each can be scaled to contain, or be contained in, any of the
others. This mutual containment of balls is exactly equivalence of topologies.

```{prf:example} Unit balls in $\mathbb{R}^n$ fit inside each other
:label: ex-rn-balls-nested

For $x \in \mathbb{R}^n$ the $\ell^p$ norms satisfy the pointwise inequalities

$$\|x\|_\infty \leq \|x\|_2 \leq \|x\|_1 \leq n\,\|x\|_\infty, \qquad
\|x\|_2 \leq \sqrt{n}\,\|x\|_\infty, \qquad \|x\|_1 \leq \sqrt{n}\,\|x\|_2.$$

Writing $B_p = \{x : \|x\|_p \leq 1\}$ for the closed unit ball of $\|\cdot\|_p$, the smaller the
norm, the larger the ball. The inequalities above translate directly into the nested inclusions

$$B_1 \subset B_2 \subset B_\infty \subset \sqrt{n}\, B_2 \subset n\, B_1.$$

So the diamond, the disk, and the square each fit inside a rescaled copy of the others. Pictorially
in $\mathbb{R}^2$: the diamond $B_1$ is inscribed in the disk $B_2$, which is inscribed in the
square $B_\infty$; conversely, the square shrunk by $\sqrt{2}$ fits back inside the disk, and the
disk shrunk by $2$ fits back inside the diamond. Because the scaling factors $1, \sqrt{n}, n$ are
*finite*, each pair of $\ell^p$ norms on $\mathbb{R}^n$ is equivalent.
```

```{prf:theorem} Equivalence of Norms in $\mathbb{R}^n$
:label: thm-rn-norms-equiv

On $\mathbb{R}^n$ all norms are equivalent.
```

```{prf:proof}
:class: dropdown

Let $\|\cdot\|$ be any norm on $\mathbb{R}^n$ and $\|\cdot\|_2$ the Euclidean norm. Writing $x =
\sum x_i e_i$ and using the triangle inequality, $\|x\| \leq \sum |x_i|\,\|e_i\| \leq b\,\|x\|_2$
where $b = (\sum \|e_i\|^2)^{1/2}$. In particular $\|\cdot\|$ is continuous with respect to
$\|\cdot\|_2$. The Euclidean unit sphere $S = \{x : \|x\|_2 = 1\}$ is compact (Heine-Borel), so the
continuous function $x \mapsto \|x\|$ attains a positive minimum $a > 0$ on $S$. Homogeneity gives
$a\|x\|_2 \leq \|x\| \leq b\|x\|_2$ for all $x$, so $\|\cdot\| \sim \|\cdot\|_2$, and hence any two
norms on $\mathbb{R}^n$ are equivalent.
```

```{prf:remark} Failure in Infinite Dimensions
:label: rem-norms-not-equiv-infinite

This theorem fails in infinite dimensions. For instance, on $\mathcal{C}^0([0,1])$ the norms
$\|\cdot\|_\infty$ and $\|\cdot\|_1$ are **not** equivalent: a sequence of tall, narrow spikes can
converge in $L^1$ without converging uniformly. The choice of norm — and hence the topology —
matters fundamentally in infinite-dimensional analysis and determines which operators are bounded,
which functionals are continuous, and which sequences converge.

The proof above breaks down exactly because the unit sphere of one norm need not be compact in the
topology of another. Equivalence of norms on $\mathbb{R}^n$ and compactness of the unit ball are
two sides of the same finite-dimensional coin.
```
