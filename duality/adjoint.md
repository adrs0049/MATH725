---
kernelspec:
  name: python3
  display_name: Python 3
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/adjoint.pdf
    id: duality-adjoint-pdf
downloads:
  - id: duality-adjoint-pdf
    title: Download PDF
---

# The Adjoint (Transpose) Operator

## The finite-dimensional picture

In $\mathbb{R}^n$, a linear map $T : \mathbb{R}^n \to \mathbb{R}^m$ is
represented by an $m \times n$ matrix $A$. The **transpose** $A^T$ is the $n
\times m$ matrix satisfying

$$\langle Ax, y \rangle = \langle x, A^T y \rangle \quad \text{for all } x \in \mathbb{R}^n, \; y \in \mathbb{R}^m.$$

The fundamental theorem of linear algebra decomposes $\mathbb{R}^n$ and
$\mathbb{R}^m$ into four mutually orthogonal subspaces:

$$\mathbb{R}^n = \ker(A) \oplus \text{Range}(A^T), \qquad \mathbb{R}^m = \ker(A^T) \oplus \text{Range}(A).$$

```{figure} /_static/fundamental_subspace.png
:name: four-subspaces-fig
:width: 80%
:align: center

The four fundamental subspaces of an $m \times n$ matrix $A$ of rank $r$. The domain $\mathbb{R}^n$ decomposes into the row space $R[A^T]$ (dimension $r$) and the nullspace $N[A]$ (dimension $n - r$), which are orthogonal complements. The codomain $\mathbb{R}^m$ decomposes into the column space $R[A]$ (dimension $r$) and the left nullspace $N[A^T]$ (dimension $m - r$), also orthogonal complements. The map $A$ sends $R[A^T]$ isomorphically onto $R[A]$, and kills $N[A]$.
```

The four subspace picture says: $A$ and $A^T$ are perfectly coupled. The kernel
of one is the orthogonal complement of the range of the other. This is the
cleanest version of the story, and it relies on two features of $\mathbb{R}^n$:

1. **Inner product:** orthogonal complements make sense.
2. **Finite dimensions:** all subspaces are closed, and ranges are automatically
   closed.

In infinite dimensions, both features can fail. The adjoint theory generalizes
this picture, but the four subspace relations require progressively more
assumptions as we move away from the finite-dimensional setting.


## The Banach adjoint (transpose)

```{prf:definition} Banach adjoint
:label: banach-adjoint-def

Let $X, Y$ be normed spaces and $T : X \to Y$ a bounded linear operator. The **adjoint** (or **transpose**) $T^* : Y^* \to X^*$ is defined by

$$(T^*g)(x) = g(Tx) \quad \text{for all } g \in Y^*, \; x \in X.$$
```

The definition is simple: $T^*$ takes a functional on $Y$ and pulls it back to a
functional on $X$ by precomposing with $T$. If $g$ defines a foliation of $Y$,
then $T^*g$ defines a foliation of $X$ whose level sets are the preimages under
$T$ of the level sets of $g$.

`````{prf:proposition} Basic properties
:label: adjoint-basic-properties

Let $T : X \to Y$ be bounded. Then:

1. $T^* : Y^* \to X^*$ is bounded with $\|T^*\| = \|T\|$.
2. $(S + T)^* = S^* + T^*$ and $(\alpha T)^* = \alpha T^*$.
3. $(ST)^* = T^* S^*$ (reversal of order).
4. $T^*$ is injective if and only if $\overline{\text{Range}(T)} = Y$.
5. $T^*$ is surjective only if $T$ is bounded below (i.e., $\|Tx\| \geq c\|x\|$ for some $c > 0$).

````{prf:proof}
:class: dropdown

**(1)** For $g \in Y^*$: $\|T^*g\| = \sup_{\|x\| \leq 1} |g(Tx)| \leq \|g\|
\cdot \|T\|$, so $\|T^*\| \leq \|T\|$. For the reverse, the {prf:ref}`sup
formula <hb-sup-formula>` gives $\|Tx\| = \sup_{\|g\| \leq 1} |g(Tx)| =
\sup_{\|g\| \leq 1} |(T^*g)(x)| \leq \|T^*\| \cdot \|x\|$, so $\|T\| \leq
\|T^*\|$.

**(3)** $((ST)^*g)(x) = g(STx) = (S^*g)(Tx) = (T^*S^*g)(x)$.

**(4)** $T^*g = 0$ means $g(Tx) = 0$ for all $x$, i.e., $g$ vanishes on
$\text{Range}(T)$. By Hahn-Banach ({prf:ref}`classification of closures
<hb-closures>`), $g$ vanishes on $\overline{\text{Range}(T)}$. So $\ker(T^*) =
\{0\}$ iff the only functional vanishing on $\overline{\text{Range}(T)}$ is
zero, iff $\overline{\text{Range}(T)} = Y$.
````
`````


## The four subspace relations: general Banach spaces

To state the four subspace relations in Banach spaces, we need a substitute for
orthogonal complements. Since we have no inner product, we use **annihilators**.

```{prf:definition} Annihilator
:label: annihilator-def

Let $X$ be a normed space.

- For $M \subseteq X$, the **annihilator** of $M$ in $X^*$ is

  $$M^\perp = \{f \in X^* : f(x) = 0 \text{ for all } x \in M\}.$$

- For $N \subseteq X^*$, the **pre-annihilator** of $N$ in $X$ is

  $${}^\perp N = \{x \in X : f(x) = 0 \text{ for all } f \in N\}.$$
```

Annihilators are the Banach-space replacement for orthogonal complements. In a
Hilbert space with Riesz identification, $M^\perp$ reduces to the usual
orthogonal complement. But in general, $M^\perp$ lives in the *dual* space, not
in $X$ itself.

`````{prf:theorem} Four subspace relations (general Banach spaces)
:label: four-subspace-general

Let $X, Y$ be Banach spaces and $T : X \to Y$ a bounded linear operator. Then:

1. $\ker(T^*) = \text{Range}(T)^\perp$
2. $\ker(T) = {}^\perp\text{Range}(T^*)$
3. $\overline{\text{Range}(T)} = {}^\perp\ker(T^*)$
4. $\overline{\text{Range}(T^*)} \subseteq \ker(T)^\perp$

````{prf:proof}
:class: dropdown

**(1)** $g \in \ker(T^*)$ iff $T^*g = 0$ iff $g(Tx) = 0$ for all $x$ iff $g \in
\text{Range}(T)^\perp$.

**(2)** $x \in {}^\perp\text{Range}(T^*)$ iff $(T^*g)(x) = 0$ for all $g \in
Y^*$ iff $g(Tx) = 0$ for all $g \in Y^*$. By the {prf:ref}`distinguishing
property <hb-separation>`, this holds iff $Tx = 0$ iff $x \in \ker(T)$.

**(3)** From (1), ${}^\perp\ker(T^*) = {}^\perp(\text{Range}(T)^\perp)$. For any
subspace $M$, the {prf:ref}`classification of closures <hb-closures>` gives
${}^\perp(M^\perp) = \overline{M}$. Applying this to $M = \text{Range}(T)$
yields (3).

**(4)** If $f \in \overline{\text{Range}(T^*)}$, then $f = \lim T^*g_n$ for some
sequence in $Y^*$. For $x \in \ker(T)$: $f(x) = \lim (T^*g_n)(x) = \lim g_n(Tx)
= 0$. So $f \in \ker(T)^\perp$.
````
`````

```{prf:remark} The asymmetry in relation (4)
:label: four-subspace-asymmetry

Relation (4) is an **inclusion**, not an equality. This is the key difference from the finite-dimensional case, and it arises because:

- In (3), we used ${}^\perp(M^\perp) = \overline{M}$, which is a theorem about $X$ (using Hahn-Banach for $X$).
- To upgrade (4) to equality, we would need $({}^\perp N)^\perp = \overline{N}$ for subspaces $N \subseteq X^*$. This requires Hahn-Banach applied to $X^*$ with functionals from $X^{**}$, and it gives $({}^\perp N)^\perp = \overline{N}^{w^*}$ (weak\* closure), which equals $\overline{N}$ (norm closure) only when $X$ is reflexive.

So in a non-reflexive space, $\text{Range}(T^*)$ can be a proper subset of $\ker(T)^\perp$ even after taking its closure. The "missing" elements of $\ker(T)^\perp$ are functionals that annihilate $\ker(T)$ but cannot be reached as limits of $T^*g_n$.
```


### The closed range theorem

The most important application of the four subspace picture is the closed range
theorem, which restores full symmetry when the range is closed.

`````{prf:theorem} Closed Range Theorem (Banach)
:label: closed-range-thm

Let $X, Y$ be Banach spaces and $T : X \to Y$ bounded. Then

$$\text{Range}(T) \text{ is closed} \iff \text{Range}(T^*) \text{ is closed.}$$

When this holds, relation (4) becomes an equality:

$$\text{Range}(T^*) = \ker(T)^\perp.$$

````{prf:proof}
:class: dropdown

**Sketch.** ($\Rightarrow$) If $\text{Range}(T)$ is closed, the open mapping
theorem applied to $T : X/\ker(T) \to \text{Range}(T)$ gives a bounded inverse.
One then shows that $T^*g_n \to f$ implies $g_n$ (restricted to
$\text{Range}(T)$) converge, producing $g$ with $T^*g = f$.

($\Leftarrow$) Apply the same argument to $T^*$.

**Equality in (4).** If $\text{Range}(T^*)$ is closed, then $\text{Range}(T^*) =
\overline{\text{Range}(T^*)} \subseteq \ker(T)^\perp$. For the reverse
inclusion: if $f \in \ker(T)^\perp$, then $f$ defines a functional on
$X/\ker(T)$. Since $T$ induces an isomorphism $X/\ker(T) \cong \text{Range}(T)$
(by the closed range), we can pull $f$ back to a functional $g$ on
$\text{Range}(T)$, extend by Hahn-Banach to $g \in Y^*$, and verify $T^*g = f$.
````
`````

The closed range condition is a property of the **operator** $T$, not the
ambient space. It is essential for solvability of equations: $Tx = y$ has a
solution iff $y \in \text{Range}(T)$, and the closed range theorem lets us check
this via the adjoint: $y \in \overline{\text{Range}(T)}$ iff $g(y) = 0$ for all
$g \in \ker(T^*)$. An alternative route to full equality in relation (4) is to
work in a reflexive space, where it holds for every bounded operator
automatically.


### Fredholm operators

The most important class of operators with closed range are the **Fredholm
operators**, where the four subspace picture is as clean as in finite
dimensions, even in non-reflexive spaces.

```{prf:definition} Fredholm operator
:label: fredholm-def

Let $X, Y$ be Banach spaces and $T : X \to Y$ a bounded linear operator. Then $T$ is **Fredholm** if:

1. $\dim \ker(T) < \infty$,
2. $\operatorname{codim} \operatorname{Range}(T) < \infty$ (equivalently, $\dim(Y / \operatorname{Range}(T)) < \infty$).

The **Fredholm index** of $T$ is

$$\operatorname{ind}(T) = \dim \ker(T) - \operatorname{codim} \operatorname{Range}(T).$$
```

The index measures the net dimensional defect of $T$: how many more dimensions
are killed than are missed.

`````{prf:theorem} Properties of Fredholm operators
:label: fredholm-properties

Let $T : X \to Y$ be Fredholm. Then:

1. $\operatorname{Range}(T)$ is closed.
2. $T^* : Y^* \to X^*$ is Fredholm with $\operatorname{ind}(T^*) = -\operatorname{ind}(T)$.
3. The four subspace relations hold with full equality:

$$\ker(T^*) = \operatorname{Range}(T)^\perp, \qquad \operatorname{Range}(T^*) = \ker(T)^\perp.$$

4. $X$ and $Y$ decompose as topological direct sums:

$$X = \ker(T) \oplus Z, \qquad Y = \operatorname{Range}(T) \oplus W,$$

where $T|_Z : Z \to \operatorname{Range}(T)$ is an isomorphism and $\dim W = \operatorname{codim} \operatorname{Range}(T)$.

````{prf:proof}
:class: dropdown

**(1)** Since $\operatorname{codim} \operatorname{Range}(T) < \infty$, there
exists a finite-dimensional subspace $W \subset Y$ with $Y =
\operatorname{Range}(T) + W$. Define $\tilde{T} : X \times W \to Y$ by
$\tilde{T}(x, w) = Tx + w$. This is bounded, linear, and surjective, so the open
mapping theorem gives $\tilde{T}$ open. It follows that
$\operatorname{Range}(T)$ is closed. (Alternatively: any subspace of finite
codimension in a Banach space is closed.)

**(2)** From (1) and the closed range theorem, $\operatorname{Range}(T^*)$ is
closed. We have $\ker(T^*) = \operatorname{Range}(T)^\perp$, so $\dim \ker(T^*)
= \operatorname{codim} \operatorname{Range}(T) < \infty$. Similarly,
$\operatorname{Range}(T^*) = \ker(T)^\perp$ (by the closed range theorem), so
$\operatorname{codim} \operatorname{Range}(T^*) = \dim \ker(T) < \infty$.
Therefore $T^*$ is Fredholm and $\operatorname{ind}(T^*) = \operatorname{codim}
\operatorname{Range}(T) - \dim \ker(T) = -\operatorname{ind}(T)$.

**(3)** Follows from (1) and the closed range theorem.

**(4)** Every finite-dimensional subspace of a Banach space is complemented. So
$\ker(T)$ has a topological complement $Z$. The restriction $T|_Z : Z \to
\operatorname{Range}(T)$ is bounded, bijective, and between Banach spaces, so
the open mapping theorem makes it an isomorphism. The complement $W$ exists
because $\operatorname{Range}(T)$ has finite codimension.
````
`````

```{prf:remark} Fredholm decomposition vs. Hilbert decomposition
:label: fredholm-vs-hilbert

The Fredholm decomposition $X = \ker(T) \oplus Z$ resembles the Hilbert space decomposition $H = \ker(T) \oplus \overline{\operatorname{Range}(T^*)}$, but the complement $Z$ is **not canonical**. There is no preferred choice without an inner product. In a Hilbert space, the orthogonal complement $\ker(T)^\perp = \overline{\operatorname{Range}(T^*)}$ provides the unique natural choice.

Despite this non-uniqueness, the Fredholm decomposition tells us that $T$ is "almost invertible" up to a finite-dimensional correction, regardless of the geometry of the ambient space.
```

`````{prf:example} Shift operators on $\ell^p$
:label: fredholm-index-example

The shift operators on $\ell^p$ ($1 \leq p < \infty$) illustrate the index:

- **Right shift** $R(x_1, x_2, \ldots) = (0, x_1, x_2, \ldots)$: injective, range has codimension 1. So $\operatorname{ind}(R) = 0 - 1 = -1$.
- **Left shift** $L(x_1, x_2, \ldots) = (x_2, x_3, \ldots)$: surjective, kernel is $\operatorname{span}\{e_1\}$. So $\operatorname{ind}(L) = 1 - 0 = 1$.

Note $L = R^*$ (under the natural pairing of $\ell^p$ and $\ell^q$), confirming $\operatorname{ind}(L) = -\operatorname{ind}(R)$. These are Fredholm on every $\ell^p$, including the non-reflexive cases $p = 1$ and $p = \infty$.
`````

```{prf:theorem} Stability of the Fredholm index
:label: fredholm-index-stability

Let $T : X \to Y$ be Fredholm.

1. **Compact perturbation:** If $K : X \to Y$ is compact, then $T + K$ is Fredholm with $\operatorname{ind}(T + K) = \operatorname{ind}(T)$.
2. **Small perturbation:** There exists $\varepsilon > 0$ such that if $\|S\| < \varepsilon$, then $T + S$ is Fredholm with $\operatorname{ind}(T + S) = \operatorname{ind}(T)$.

In particular, the Fredholm index is a topological invariant: it is constant on connected components of the set of Fredholm operators.
```

The stability theorem is why the Fredholm index matters: it is computable (often
by deformation to a simpler operator) and robust under perturbation. This makes
it the central tool in index theory, where one relates the analytic index of a
differential operator to topological data of the underlying manifold.


## Reflexive spaces: full symmetry restored

In a reflexive space ($X \cong X^{**}$ via the canonical embedding), the
asymmetry in relation (4) disappears.

`````{prf:theorem} Four subspace relations (reflexive spaces)
:label: four-subspace-reflexive

Let $X, Y$ be **reflexive** Banach spaces and $T : X \to Y$ bounded. Then all four relations hold with equality:

1. $\ker(T^*) = \text{Range}(T)^\perp$
2. $\ker(T) = {}^\perp\text{Range}(T^*)$
3. $\overline{\text{Range}(T)} = {}^\perp\ker(T^*)$
4. $\overline{\text{Range}(T^*)} = \ker(T)^\perp$

````{prf:proof}
:class: dropdown

Relations (1)--(3) hold in any Banach space. For (4): in a reflexive space,
every functional on $X^*$ comes from an element of $X$, so the weak\* closure
and the norm closure of any convex subset of $X^*$ coincide. Therefore
$({}^\perp N)^\perp = \overline{N}$ for subspaces $N \subseteq X^*$, and
applying this to $N = \text{Range}(T^*)$ gives $\ker(T)^\perp =
({}^\perp\text{Range}(T^*))^\perp = \overline{\text{Range}(T^*)}$.
````
`````

Reflexivity restores the full symmetry of the finite-dimensional picture: each
kernel is the annihilator of the other's range, and vice versa. No closed range
assumption is needed for the four relations to hold (though the ranges
themselves may still not be closed).


## Hilbert spaces: orthogonal complements

In a Hilbert space, the Riesz representation theorem identifies $H^*$ with $H$,
and annihilators become orthogonal complements. The Banach adjoint $T^*$ becomes
the **Hilbert adjoint**, defined by the familiar relation:

```{prf:definition} Hilbert adjoint
:label: hilbert-adjoint-def

Let $H, K$ be Hilbert spaces and $T : H \to K$ a bounded linear operator. The **Hilbert adjoint** $T^* : K \to H$ is the unique operator satisfying

$$\langle Tx, y \rangle_K = \langle x, T^*y \rangle_H \quad \text{for all } x \in H, \; y \in K.$$
```

The Hilbert adjoint maps back into the *same type of space* (not the dual),
which is why we can write the four subspace decompositions as orthogonal direct
sums within $H$ and $K$ themselves.

`````{prf:corollary} Four subspaces in Hilbert space
:label: four-subspace-hilbert

Let $H, K$ be Hilbert spaces and $T : H \to K$ bounded. Then:

$$H = \ker(T) \oplus \overline{\text{Range}(T^*)}, \qquad K = \ker(T^*) \oplus \overline{\text{Range}(T)}.$$

The four subspaces satisfy:

1. $\ker(T^*) = \text{Range}(T)^\perp$
2. $\ker(T) = \text{Range}(T^*)^\perp$
3. $\overline{\text{Range}(T)} = \ker(T^*)^\perp$
4. $\overline{\text{Range}(T^*)} = \ker(T)^\perp$

All orthogonal complements are taken in the ambient Hilbert space (not the dual).
`````

This is exactly the finite-dimensional picture, with closures added to account
for the possibility that ranges are not closed. Every vector in $H$ decomposes
uniquely into a component killed by $T$ and a component in the closure of what
$T^*$ produces.

```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import matplotlib.pyplot as plt

fig, ax = plt.subplots(figsize=(10, 5))

# Draw domain box (H)
ax.add_patch(plt.Rectangle((0.5, 0.5), 3, 4, fill=False, edgecolor='gray',
                            lw=2, ls='--'))
ax.text(2.0, 4.7, r'$H$', fontsize=16, ha='center', color='gray')

# ker(T) horizontal band
ax.fill_between([0.7, 3.3], 1.0, 2.3, color='C0', alpha=0.15)
ax.text(2.0, 1.65, r'$\ker(T)$', fontsize=13, ha='center', color='C0')

# Range(T*) vertical band
ax.fill_between([0.7, 3.3], 2.7, 4.0, color='C1', alpha=0.15)
ax.text(2.0, 3.35, r'$\overline{\mathrm{Range}(T^*)}$', fontsize=13,
        ha='center', color='C1')

# Orthogonality symbol
ax.text(2.0, 2.5, r'$\perp$', fontsize=14, ha='center', color='black')

# Arrow T
ax.annotate('', xy=(6.5, 2.5), xytext=(4.0, 2.5),
            arrowprops=dict(arrowstyle='->', color='black', lw=2.5))
ax.text(5.25, 2.8, r'$T$', fontsize=16, ha='center')

# Draw codomain box (K)
ax.add_patch(plt.Rectangle((7.0, 0.5), 3, 4, fill=False, edgecolor='gray',
                            lw=2, ls='--'))
ax.text(8.5, 4.7, r'$K$', fontsize=16, ha='center', color='gray')

# ker(T*) horizontal band
ax.fill_between([7.2, 9.8], 1.0, 2.3, color='C2', alpha=0.15)
ax.text(8.5, 1.65, r'$\ker(T^*)$', fontsize=13, ha='center', color='C2')

# Range(T) vertical band
ax.fill_between([7.2, 9.8], 2.7, 4.0, color='C3', alpha=0.15)
ax.text(8.5, 3.35, r'$\overline{\mathrm{Range}(T)}$', fontsize=13,
        ha='center', color='C3')

ax.text(8.5, 2.5, r'$\perp$', fontsize=14, ha='center', color='black')

# Arrow T*
ax.annotate('', xy=(4.0, 1.5), xytext=(6.5, 1.5),
            arrowprops=dict(arrowstyle='->', color='black', lw=2.5))
ax.text(5.25, 1.1, r'$T^*$', fontsize=16, ha='center')

ax.set_xlim(0, 11)
ax.set_ylim(0, 5.2)
ax.set_aspect('equal')
ax.axis('off')
ax.set_title('The four subspace picture in Hilbert space', fontsize=13)

plt.tight_layout()
plt.show()
```

*The four subspace decomposition. $T$ maps $\overline{\mathrm{Range}(T^*)}$ into
$\overline{\mathrm{Range}(T)}$ and kills $\ker(T)$. $T^*$ maps
$\overline{\mathrm{Range}(T)}$ into $\overline{\mathrm{Range}(T^*)}$ and kills
$\ker(T^*)$. Each pair is an orthogonal complement in its ambient Hilbert
space.*

