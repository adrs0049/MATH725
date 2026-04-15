---
kernelspec:
  name: python3
  display_name: Python 3
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/fredholm.pdf
    id: duality-fredholm-pdf
downloads:
  - id: duality-fredholm-pdf
    title: Download PDF
---

# Application: Fredholm Operators

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
:class: dropdown

The Fredholm decomposition $X = \ker(T) \oplus Z$ guarantees that *some* closed
complement $Z$ exists (since $\ker(T)$ is finite-dimensional), but there are
infinitely many such $Z$. For example, if $\ker(T) = \operatorname{span}\{v\}$
in $\mathbb{R}^2$, then any line not parallel to $v$ is a valid complement, and
each gives a different projection onto $\ker(T)$: the same vector $x$
decomposes differently depending on which $Z$ we choose. Without an inner
product, no choice is preferred.

In a Hilbert space, the inner product singles out the **orthogonal** complement
$Z = \ker(T)^\perp$: the unique complement for which the projection is
self-adjoint (equivalently, the decomposition $x = x_{\ker} + x_Z$ minimizes
$\|x_Z\|$). The four subspace theorem identifies this canonical choice
concretely as $\ker(T)^\perp = \overline{\operatorname{Range}(T^*)}$ — the
closure of what $T^*$ produces.

Despite the non-uniqueness of $Z$ in a general Banach space, the Fredholm
decomposition still tells us that $T$ is "almost invertible" up to a
finite-dimensional correction, regardless of the geometry of the ambient space.
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

```{prf:remark} The Fredholm alternative
:label: fredholm-alternative
:class: dropdown

For any Fredholm operator $T : X \to Y$, the solvability condition

$$
Tx = y \text{ is solvable} \iff \psi(y) = 0 \text{ for all } \psi \in \ker(T^*)
$$

holds, since $\operatorname{Range}(T)$ is closed and $\ker(T^*) =
\operatorname{Range}(T)^\perp$ by {prf:ref}`fredholm-properties`. However, the
classical **Fredholm alternative** — the dichotomy that $T$ is either bijective
or has a nontrivial kernel — requires $\operatorname{ind}(T) = 0$. When the
index is zero, $\dim\ker(T) = \operatorname{codim}\operatorname{Range}(T)$, so
injectivity and surjectivity are equivalent: either both hold (and $T$ is
bijective) or neither does.

For nonzero index this dichotomy fails. The right shift $R$ on $\ell^p$
({prf:ref}`fredholm-index-example`) is injective but not surjective:
$\ker(R) = \{0\}$ yet $\operatorname{codim}\operatorname{Range}(R) = 1$. There
is no contradiction with the solvability condition — $Rx = y$ is solvable if
and only if $y \perp \ker(R^*) = \operatorname{span}\{e_1^*\}$, i.e., $y_1 =
0$ — but the "either bijective or..." structure is lost.
```


### Solvability conditions

The solvability condition from {prf:ref}`fredholm-alternative` is one of the
most useful consequences of Fredholm theory in PDE applications. We state it
explicitly.

`````{prf:corollary} Fredholm solvability condition
:label: fredholm-solvability

Let $T : X \to Y$ be a Fredholm operator with $\ker(T^*) =
\operatorname{span}\{\psi_1, \ldots, \psi_m\}$. Then the equation $Tx = f$ has
a solution if and only if

$$
\psi_j(f) = 0, \qquad j = 1, \ldots, m.
$$

When a solution exists, it is unique up to an element of $\ker(T)$: the general
solution is $x = x_p + \sum_{i=1}^n \alpha_i v_i$, where $x_p$ is any
particular solution, $\{v_1, \ldots, v_n\}$ is a basis of $\ker(T)$, and the
$\alpha_i$ are arbitrary.

````{prf:proof}
:class: dropdown

$Tx = f$ is solvable iff $f \in \operatorname{Range}(T)$. Since $T$ is
Fredholm, $\operatorname{Range}(T)$ is closed ({prf:ref}`fredholm-properties`),
so $\operatorname{Range}(T) = {}^\perp\ker(T^*)$ by
{prf:ref}`four-subspace-general`. Therefore $f \in \operatorname{Range}(T)$ iff
$\psi(f) = 0$ for all $\psi \in \ker(T^*)$, which is equivalent to $\psi_j(f) =
0$ for each basis element.
````
`````

In PDE applications, the $\psi_j$ are typically known explicitly (from the
symmetry or structure of the problem), and the solvability conditions take the
form of **integral constraints** on the data.

`````{prf:example} Solvability of the Neumann problem
:label: neumann-solvability

Consider the Neumann problem for Poisson's equation on a bounded Lipschitz
domain $\Omega \subset \mathbb{R}^d$:

$$
-\Delta u = f \quad \text{in } \Omega, \qquad \frac{\partial u}{\partial n} = 0 \quad \text{on } \partial\Omega.
$$

Formulated weakly, the operator $T = -\Delta_N : H^1(\Omega) \to H^1(\Omega)^*$
defined by

$$
\langle Tu, v \rangle = \int_\Omega \nabla u \cdot \nabla v \, dx
$$

is Fredholm with index zero:

- **Kernel.** $\ker(T) = \operatorname{span}\{1\}$: the constant functions, since
  $\int_\Omega |\nabla u|^2 \, dx = 0$ implies $u$ is constant.
- **Cokernel.** By self-adjointness, $\ker(T^*) = \ker(T) =
  \operatorname{span}\{1\}$, so $\operatorname{codim}
  \operatorname{Range}(T) = 1$.

By {prf:ref}`fredholm-solvability`, $-\Delta_N u = f$ has a solution if and only
if $\psi(f) = 0$ for the single cokernel element $\psi = 1$:

$$
\int_\Omega f \, dx = 0 \qquad \text{(the data must have zero mean).}
$$

This is the classical compatibility condition: by the divergence theorem,
$\int_\Omega \Delta u\, dx = \int_{\partial\Omega} \frac{\partial u}{\partial
n}\, dS = 0$, so $\int_\Omega f\, dx = 0$ is necessary. Fredholm theory shows
it is also sufficient. When satisfied, the solution is unique up to an additive
constant.
`````

The Fredholm index is $\operatorname{ind}(T) = 1 - 1 = 0$, but $T$ is not
invertible. To obtain a well-posed problem, we must simultaneously *impose a
constraint* to select a unique solution (pin the constant) and *add a degree of
freedom* to absorb right-hand sides that violate the compatibility condition.

### The bordered operator

```{prf:definition} Bordered operator
:label: bordered-operator-def

Let $T : X \to Y$ be Fredholm with $\operatorname{ind}(T) = 0$ and $n = \dim
\ker(T)$. Let $\{\phi_1, \ldots, \phi_n\} \subset Y$ and $\{\ell_1, \ldots,
\ell_n\} \subset X^*$. The **bordered operator** is

$$
\widehat{T} =
\begin{pmatrix}
T & \Phi \\
L & 0
\end{pmatrix}
: X \times \mathbb{R}^n \to Y \times \mathbb{R}^n,
$$

where $\Phi : \mathbb{R}^n \to Y$ maps $\alpha \mapsto \sum_{j=1}^n \alpha_j \phi_j$ and $L : X \to \mathbb{R}^n$ maps $x \mapsto (\ell_1(x), \ldots, \ell_n(x))$.

The bordered system $\widehat{T}(x, \alpha) = (y, c)$ reads:

$$
Tx + \sum_{j=1}^n \alpha_j \phi_j = y, \qquad \ell_j(x) = c_j, \quad j = 1, \ldots, n.
$$
```

The idea is transparent: the functionals $\ell_j$ select a unique element of
$\ker(T)$ (by prescribing the "coordinates" $c_j$), and the vectors $\phi_j$
span a complement to $\operatorname{Range}(T)$, so the extra unknowns $\alpha_j$
allow us to absorb the component of $y$ outside the range.

`````{prf:theorem} Invertibility of the bordered operator
:label: bordered-invertible

Let $T : X \to Y$ be Fredholm with $\operatorname{ind}(T) = 0$ and $n = \dim
\ker(T)$. Let $\{v_1, \ldots, v_n\}$ be a basis of $\ker(T)$ and $\{\psi_1,
\ldots, \psi_n\} \subset Y^*$ a basis of $\ker(T^*)$. Then the bordered
operator $\widehat{T}$ is boundedly invertible if and only if:

1. **The $\ell_j$ detect the kernel:** the $n \times n$ matrix $M_{ij} =
   \ell_i(v_j)$ is invertible.
2. **The $\phi_j$ complement the range:** the $n \times n$ matrix $N_{ij} =
   \psi_i(\phi_j)$ is invertible.

````{prf:proof}
:class: dropdown

By {prf:ref}`fredholm-properties`, the spaces decompose as

$$
X = \ker(T) \oplus Z, \qquad Y = \operatorname{Range}(T) \oplus W,
$$

where $T|_Z : Z \to \operatorname{Range}(T)$ is an isomorphism and $W$ has
dimension $n$.

**Injectivity.** Suppose $\widehat{T}(x, \alpha) = (0, 0)$. The second
component gives $\ell_j(x) = 0$ for all $j$. The first gives $Tx = -\sum
\alpha_j \phi_j$. Applying each $\psi_i \in \ker(T^*) =
\operatorname{Range}(T)^\perp$ to the first equation:

$$
0 = \psi_i(Tx) = -\sum_{j=1}^n \alpha_j \psi_i(\phi_j) = -(N\alpha)_i.
$$

Since $N$ is invertible by assumption (2), $\alpha = 0$. Therefore $Tx = 0$, so
$x \in \ker(T)$. Writing $x = \sum \beta_j v_j$, we have $\ell_i(x) = \sum
\beta_j \ell_i(v_j) = (M\beta)_i = 0$. Since $M$ is invertible by assumption
(1), $\beta = 0$, hence $x = 0$.

**Surjectivity.** Given $(y, c) \in Y \times \mathbb{R}^n$, we must find $(x,
\alpha)$ such that $Tx + \sum \alpha_j \phi_j = y$ and $\ell_j(x) = c_j$.

*Step 1.* Decompose $y = y_R + y_W$ with $y_R \in \operatorname{Range}(T)$ and
$y_W \in W$. Since $\{\psi_i\}$ is a basis for $\operatorname{Range}(T)^\perp$,
the coordinates of $y_W$ relative to the $\phi_j$ are determined by $\psi_i(y) =
\sum \alpha_j \psi_i(\phi_j)$, i.e., $\alpha = N^{-1}(\psi_1(y), \ldots,
\psi_n(y))^T$. With this choice, $y - \sum \alpha_j \phi_j \in
\operatorname{Range}(T)$.

*Step 2.* Since $T|_Z$ is an isomorphism onto $\operatorname{Range}(T)$, there
exists a unique $z \in Z$ with $Tz = y - \sum \alpha_j \phi_j$.

*Step 3.* Set $x = z + \sum \beta_j v_j$ where $\beta = M^{-1}(c_1 -
\ell_1(z), \ldots, c_n - \ell_n(z))^T$. Then $Tx = Tz = y - \sum \alpha_j
\phi_j$ and $\ell_i(x) = \ell_i(z) + (M\beta)_i = c_i$.

**Bounded inverse.** $\widehat{T}$ is a bounded bijection between Banach
spaces, so the open mapping theorem gives a bounded inverse.
````
`````

```{prf:remark}
:label: bordered-practical
:class: dropdown

The conditions are easy to check in practice. Condition (1) says: the
constraints $\ell_j$ must be *linearly independent when restricted to the
kernel*. Condition (2) says: the vectors $\phi_j$ must be *transverse to the
range*, i.e., they span a complement. When $T$ is self-adjoint (so $\ker(T) =
\ker(T^*)$), a natural choice is $\phi_j = v_j$ — use the kernel elements
themselves to span the cokernel complement.
```

`````{prf:example} Bordered Neumann Laplacian
:label: bordered-neumann

Returning to the Neumann Laplacian $T = -\Delta_N$ with $n = 1$:

- **Kernel basis:** $v_1 = 1$ (the constant function).
- **Cokernel basis:** $\psi_1 = \frac{1}{|\Omega|}\int_\Omega (\cdot)\, dx$
  (the mean functional), since $T$ is self-adjoint.

Choose $\phi_1 = 1$ and $\ell_1(u) = \frac{1}{|\Omega|}\int_\Omega u\, dx$. Then:

- $M_{11} = \ell_1(v_1) = \frac{1}{|\Omega|}\int_\Omega 1\, dx = 1 \neq 0$. ✓
- $N_{11} = \psi_1(\phi_1) = \frac{1}{|\Omega|}\int_\Omega 1\, dx = 1 \neq 0$. ✓

By {prf:ref}`bordered-invertible`, the bordered operator

$$
\widehat{T} =
\begin{pmatrix}
-\Delta_N & 1 \\[4pt]
\displaystyle\frac{1}{|\Omega|}\int_\Omega (\cdot)\, dx & 0
\end{pmatrix}
$$

is invertible. The bordered system

$$
-\Delta u + \lambda = f, \qquad \frac{1}{|\Omega|}\int_\Omega u\, dx = 0,
$$

has a unique solution $(u, \lambda)$ for every $f \in H^1(\Omega)^*$. The
constraint pins the mean of $u$ to zero, and the Lagrange multiplier $\lambda =
\frac{1}{|\Omega|}\int_\Omega f\, dx$ absorbs the mean of $f$.

````{prf:proof}
:class: dropdown

That $\lambda = \frac{1}{|\Omega|}\int_\Omega f\, dx$ follows by integrating the
first equation: $-\int_\Omega \Delta u\, dx + \lambda|\Omega| = \int_\Omega
f\, dx$. By the divergence theorem and the Neumann condition, $\int_\Omega
\Delta u\, dx = \int_{\partial\Omega} \frac{\partial u}{\partial n}\, dS = 0$,
so $\lambda = \frac{1}{|\Omega|}\int_\Omega f\, dx$.
````
`````

### Solving the bordered system by block elimination

The bordered system can be solved using $T$ and $T^*$ as **black boxes** — we
never form the bordered matrix, only call the forward and adjoint solvers.
Consider the general bordered system

$$
\begin{pmatrix} T & \phi \\ \ell & 0 \end{pmatrix}
\begin{pmatrix} x \\ \lambda \end{pmatrix}
= \begin{pmatrix} f \\ c \end{pmatrix},
$$

where $T : X \to Y$ is Fredholm with index zero, $\dim\ker(T) = 1$, $v \in
\ker(T)$, and $\psi \in \ker(T^*)$. The algorithm is a walk through the four
subspace decomposition:

$$
X = \ker(T) \oplus Z, \qquad Y = \operatorname{Range}(T) \oplus \ker(T^*).
$$

**Step 1: Project $f$ onto $\ker(T^*)$ to determine $\lambda$.**
The right-hand side $f \in Y$ decomposes as $f = f_R + f_\perp$ with $f_R \in
\operatorname{Range}(T)$ and $f_\perp \in \ker(T^*)$. Apply $\psi \in
\ker(T^*) = \operatorname{Range}(T)^\perp$ to the first row: $\psi(Tx +
\lambda\phi) = \psi(f)$. Since $\psi(Tx) = (T^*\psi)(x) = 0$, this kills the
$\operatorname{Range}(T)$ component entirely and reads off the
$\ker(T^*)$ component:

$$
\lambda = \frac{\psi(f)}{\psi(\phi)}.
$$

The denominator $\psi(\phi) \neq 0$ is the transversality condition from
{prf:ref}`bordered-invertible`: $\phi$ is not in $\operatorname{Range}(T)$, so
$\psi$ sees it. This works for **any** $f$ — the multiplier $\lambda$
absorbs whatever component of $f$ lies outside $\operatorname{Range}(T)$.

**Step 2: Solve in $\operatorname{Range}(T)$ for a particular solution.**
By construction, $f - \lambda\phi$ has no $\ker(T^*)$ component: Step 1 chose
$\lambda$ precisely so that $f - \lambda\phi \in \operatorname{Range}(T)$.
The restriction $T|_Z : Z \to \operatorname{Range}(T)$ is an isomorphism
({prf:ref}`fredholm-properties`), so the black-box solver returns the unique
$x_p \in Z$ with

$$
T x_p = f - \lambda \phi.
$$

This is one call to the forward solver. The solution $x_p$ lies in the
complement $Z$ of $\ker(T)$, but a general solver may return $x_p$ only up to
an element of $\ker(T)$ — the next step handles this.

**Step 3: Project onto $\ker(T)$ using the constraint.**
The general solution of the first row is $x = x_p + \alpha v$, decomposed
along $X = \ker(T) \oplus Z$. The parameter $\alpha$ is the $\ker(T)$
component, which $T$ cannot see. The second row $\ell(x) = c$ determines it:

$$
\alpha = \frac{c - \ell(x_p)}{\ell(v)}.
$$

The denominator $\ell(v) \neq 0$ is the detection condition from
{prf:ref}`bordered-invertible`: $\ell$ is nontrivial on $\ker(T)$. The
solution is $x = x_p + \alpha v$, $\lambda$ from Step 1.

`````{prf:example} Block elimination for the Neumann Laplacian
:label: bordered-neumann-solve

For the Neumann Laplacian $T = -\Delta_N$ with $v = 1$, $\psi = \ell =
\frac{1}{|\Omega|}\int_\Omega (\cdot)\, dx$, and $\phi = 1$:

- **Step 1.** Project onto $\ker(T^*) = \operatorname{span}\{1\}$: $\lambda =
  \psi(f)/\psi(\phi) = \frac{1}{|\Omega|}\int_\Omega f\, dx$, the mean of $f$.
  This extracts the incompatible component of $f$.
- **Step 2.** Solve in $\operatorname{Range}(T)$: $-\Delta_N u_p = f - \lambda$.
  The right-hand side has zero mean by construction, so this is a compatible
  Neumann problem for any $f$.
- **Step 3.** Project onto $\ker(T) = \operatorname{span}\{1\}$: $\alpha = (c -
  \ell(u_p))/\ell(1) = c - \frac{1}{|\Omega|}\int_\Omega u_p\, dx$, and $u =
  u_p + \alpha$.

Setting $c = 0$ pins the mean of $u$ to zero.
`````

```{prf:remark}
:label: bordered-general-fredholm
:class: dropdown

The bordered operator technique is not limited to index-zero operators or to
self-adjoint problems. For a general Fredholm operator with $\operatorname{ind}(T)
= k \neq 0$, one can still form a bordered system, but the sizes of $\Phi$ and
$L$ differ: if $\dim\ker(T) = n$ and $\operatorname{codim}\operatorname{Range}(T)
= m$ (with $n - m = k$), then

$$
\widehat{T} =
\begin{pmatrix}
T & \Phi \\
L & 0
\end{pmatrix}
: X \times \mathbb{R}^m \to Y \times \mathbb{R}^n
$$

is invertible under the analogous transversality and detection conditions. The
rectangular bordering reflects the dimensional mismatch measured by the index.
```
