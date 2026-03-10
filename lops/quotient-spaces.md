---
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/quotient-spaces.pdf
    id: lops-quotient-spaces-pdf
downloads:
  - id: lops-quotient-spaces-pdf
    title: Download PDF
---

# Quotient Spaces and Codimension

When we study a linear operator $T : X \to Y$, its kernel $\ker(T)$ captures
what $T$ "forgets." The quotient space $X / \ker(T)$ is the space that remains
after collapsing everything $T$ cannot distinguish.

## Quotient Spaces

```{prf:definition} Quotient space
:label: quotient-space

Let $X$ be a vector space and $M \subset X$ a subspace. The **quotient space**
$X / M$ is the set of equivalence classes

$$[x] = x + M = \{x + m : m \in M\}$$

under the equivalence relation $x \sim y \iff x - y \in M$. This is a vector
space with operations

$$[x] + [y] = [x + y], \qquad \lambda [x] = [\lambda x].$$

The **canonical projection** $\pi : X \to X/M$ defined by $\pi(x) = [x]$ is a
surjective linear map with $\ker(\pi) = M$.
```

The elements of $X/M$ are the "cosets" or translates $x + M$. Two vectors $x$
and $y$ represent the same coset precisely when $x - y \in M$ — that is, when
they differ by something in $M$.

```{prf:example} Quotient in $\mathbb{R}^3$
:label: quotient-R3

Let $X = \mathbb{R}^3$ and $M = \{(x,y,0) : x, y \in \mathbb{R}\}$ (the
$xy$-plane). Then $X/M \cong \mathbb{R}$: each coset is a horizontal plane at
height $z$, and the quotient map sends $(x,y,z) \mapsto z$. All the
$x$- and $y$-information is "collapsed" — only the height survives.
```

```{prf:example} Quotient by a kernel
:label: quotient-kernel-example

Let $f : \mathbb{R}^3 \to \mathbb{R}$ be defined by $f(x,y,z) = 2x + 3y - z$.
Then $\ker(f) = \{2x + 3y - z = 0\}$ is a plane through the origin. The cosets
of $\ker(f)$ are the level sets $f^{-1}(c) = \{2x + 3y - z = c\}$ — parallel
planes, each labeled by the value $c$. The quotient $\mathbb{R}^3 / \ker(f)$ is
one-dimensional, reflecting the fact that $f$ maps onto $\mathbb{R}$.
```

### The quotient norm

When $X$ is a normed space and $M$ is a **closed** subspace, the quotient
inherits a natural norm.

```{prf:definition} Quotient norm
:label: quotient-norm

Let $X$ be a normed space and $M \subset X$ a closed subspace. The **quotient
norm** on $X/M$ is

$$\|[x]\|_{X/M} = \inf_{m \in M} \|x - m\| = \operatorname{dist}(x, M).$$
```

The closedness of $M$ ensures this is a genuine norm (not just a seminorm): if
$\|[x]\|_{X/M} = 0$, then $\operatorname{dist}(x, M) = 0$, so $x \in
\overline{M} = M$, hence $[x] = [0]$.

````{prf:proposition}
:label: quotient-banach

If $X$ is a Banach space and $M \subset X$ is a closed subspace, then $X/M$ is a
Banach space.

```{prf:proof}
:class: dropdown

Let $([x_n])$ be a Cauchy sequence in $X/M$. Passing to a subsequence, we may
assume $\|[x_{n+1}] - [x_n]\|_{X/M} < 2^{-n}$. By definition of the infimum,
choose representatives: pick $y_1 = x_1$, and for each $n$ pick $m_n \in M$ such
that $\|x_{n+1} - x_n - m_n\| < 2^{-n}$. Define $y_{n+1} = x_{n+1} - (m_1 +
\cdots + m_n)$; then $[y_n] = [x_n]$ and $\|y_{n+1} - y_n\| < 2^{-n}$, so
$(y_n)$ is Cauchy in $X$. Since $X$ is complete, $y_n \to y$ for some $y \in X$.
Then $[x_n] = [y_n] \to [y]$ in $X/M$.
```
````


## Codimension

```{prf:definition} Codimension
:label: codimension

Let $M$ be a subspace of a vector space $X$. The **codimension** of $M$ in $X$
is

$$\operatorname{codim}(M) = \dim(X / M).$$

Equivalently, $\operatorname{codim}(M) = k$ means there exist vectors $e_1,
\ldots, e_k \in X$ such that

$$X = M \oplus \operatorname{span}(e_1, \ldots, e_k),$$

and $k$ is the smallest number for which such a decomposition exists.
```

Codimension measures how many dimensions are "missing" from $M$. A
codimension-1 subspace is as large as possible while still being proper — it is
a **hyperplane** through the origin.

```{prf:example}
In $\mathbb{R}^n$:
- A line through the origin has codimension $n - 1$.
- A plane through the origin in $\mathbb{R}^3$ has codimension $1$.
- The subspace $\{0\}$ has codimension $n$.
```


## The First Isomorphism Theorem

````{prf:theorem} First Isomorphism Theorem
:label: first-isomorphism-theorem

Let $T : X \to Y$ be a linear map. Then $T$ induces an isomorphism

$$\widetilde{T} : X / \ker(T) \xrightarrow{\;\cong\;} \operatorname{Range}(T)$$

defined by $\widetilde{T}([x]) = Tx$. This map is well-defined, linear,
injective, and surjective onto $\operatorname{Range}(T)$.

If $X$ and $Y$ are Banach spaces, $T$ is bounded, and $\operatorname{Range}(T)$
is closed, then $\widetilde{T}$ is a topological isomorphism (i.e., $\widetilde{T}$
and $\widetilde{T}^{-1}$ are both bounded). This follows from the
{prf:ref}`thm-open-mapping` applied to the bijective bounded operator
$\widetilde{T}$.

```{prf:proof}
:class: dropdown

**Well-defined:** If $[x_1] = [x_2]$, then $x_1 - x_2 \in \ker(T)$, so $Tx_1 =
Tx_2$.

**Linear:** $\widetilde{T}(\alpha[x] + \beta[y]) = \widetilde{T}([\alpha x +
\beta y]) = T(\alpha x + \beta y) = \alpha Tx + \beta Ty = \alpha
\widetilde{T}([x]) + \beta \widetilde{T}([y])$.

**Injective:** $\widetilde{T}([x]) = 0 \implies Tx = 0 \implies x \in \ker(T)
\implies [x] = [0]$.

**Surjective onto $\operatorname{Range}(T)$:** For any $y = Tx \in
\operatorname{Range}(T)$, we have $\widetilde{T}([x]) = y$.

**Bounded (when $T$ is bounded):** For any $m \in \ker(T)$, $\|Tx\| =
\|T(x-m)\| \leq \|T\|\|x - m\|$. Taking the infimum over $m$:
$\|\widetilde{T}([x])\| \leq \|T\| \, \|[x]\|$. So $\|\widetilde{T}\| \leq
\|T\|$.
```
````

The first isomorphism theorem immediately answers the question: *why does a
nonzero linear functional have a codimension-1 kernel?*

````{prf:corollary}
:label: kernel-codim-1

Let $f : X \to \mathbb{R}$ be a nonzero linear functional. Then
$\operatorname{codim}(\ker(f)) = 1$.

```{prf:proof}
:class: dropdown

Since $f$ is nonzero, there exists $x_0 \in X$ with $f(x_0) \neq 0$. For any $c
\in \mathbb{R}$, we have $f(cx_0 / f(x_0)) = c$, so $f$ is surjective. By the
first isomorphism theorem ({prf:ref}`first-isomorphism-theorem`),

$$X / \ker(f) \cong \operatorname{Range}(f) = \mathbb{R}.$$

Therefore $\operatorname{codim}(\ker(f)) = \dim(X / \ker(f)) = \dim(\mathbb{R})
= 1$.
```
````

The key insight: the codimension equals $1$ because the **target** is
$\mathbb{R}$, which is one-dimensional. The first isomorphism theorem tells us
that the quotient $X / \ker(f)$ is isomorphic to the range, and since $f$ maps
onto all of $\mathbb{R}$, the quotient is one-dimensional — regardless of
whether $X$ itself is finite- or infinite-dimensional.
