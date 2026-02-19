---
exports:
  - format: pdf
    template: plain_latex
    output: exports/compact.pdf
    id: lops-compact-pdf
downloads:
  - id: lops-compact-pdf
    title: Download PDF
---

# Compact Operators

In finite dimensions, every linear operator maps bounded sets to bounded sets, and since
closed bounded sets are compact (Heine-Borel), bounded sequences always have convergent
subsequences. This is the engine behind most of finite-dimensional linear algebra: eigenvalue
decompositions, the SVD, and the Fredholm alternative all rely on extracting convergent subsequences.

In infinite dimensions, closed bounded sets are **no longer compact**
({prf:ref}`ex-unit-ball-l2-not-compact`), and this machinery breaks down for general bounded
operators. Compact operators are precisely the class of operators for which it **does not break
down**—they are the infinite-dimensional operators that still behave like matrices.

::::{dropdown} **Why is extracting convergent subsequences the engine behind finite-dimensional linear algebra?**

The eigenvalue decomposition and the SVD both reduce to finding a vector that **achieves an
extremum**. The method is always:

1. Take a sequence approaching the supremum/infimum.
2. **Extract a convergent subsequence** (compactness of the unit ball).
3. The limit achieves the optimum (continuity).

**Eigenvalues** of a symmetric matrix are found by maximizing the Rayleigh quotient
$R(x) = \langle Ax, x \rangle / \|x\|^2$ over the unit sphere. In $\mathbb{R}^n$ the unit sphere
is compact, so a maximizing sequence has a convergent subsequence whose limit is an eigenvector.
Restrict to its orthogonal complement and repeat—the full eigenvalue decomposition follows by
induction. Each eigenvalue $\lambda_i$ yields a projection $P_i = \langle \cdot, \psi_i \rangle
\psi_i$ onto the corresponding eigenspace, and the spectral decomposition $A = \sum \lambda_i P_i$
says the operator is a sum of scaled orthogonal projections.

**The SVD** of a general (non-symmetric) matrix follows the same pattern by reducing to the
symmetric case: form $K^*K$ (which is self-adjoint and positive), apply the Rayleigh quotient
argument to find its eigenvalues $\sigma_i^2$ and eigenvectors $v_i$, then set
$u_i = Kv_i / \sigma_i$. The result is $K = \sum \sigma_i \langle \cdot, v_i \rangle \, u_i$.
Each step requires extracting a convergent subsequence from a maximizing sequence on the unit sphere.

:::{admonition} What breaks in infinite dimensions
:class: warning

The unit ball in an infinite-dimensional Banach space is not compact
({prf:ref}`ex-unit-ball-l2-not-compact`), so step 2 fails. This is why general bounded operators
need not have eigenvalues (e.g. the right shift on $\ell^2$), and why the spectrum can have
continuous and residual parts with no finite-dimensional analogue.
:::

A compact operator maps bounded sequences to sequences with convergent subsequences—**by
definition**. This is step 2, transplanted from a property of the space to a property of the
operator. For the Hilbert-Schmidt spectral theorem, you maximize the Rayleigh quotient on the unit
sphere. You cannot extract a convergent subsequence from the maximizing sequence $(x_n)$ directly,
but since $A$ is compact, $(Ax_n)$ has a convergent subsequence, which suffices to show $(x_n)$
converges to an eigenvector. Compactness of the operator substitutes for compactness of the ball.

::::

## Definition and Basic Properties

```{prf:definition} Compact operator
:label: def-compact-operator

An operator $K : X \to Y$ between normed spaces is **compact** if for each bounded set
$U \subset X$, the image $K(U)$ is relatively compact in $Y$ (i.e., $\overline{K(U)}$ is compact).

Equivalently, $K$ is compact if and only if every bounded sequence $(x_n)$ in $X$ has a
subsequence $(x_{n_k})$ such that $(Kx_{n_k})$ converges in $Y$.
```

The sequential characterization is the one we use most often in practice: **bounded sequence in,
convergent subsequence out**. Compare this with a general bounded operator, which only guarantees
bounded sequence in, bounded sequence out.

```{prf:proposition} Compact operators are bounded
:label: prop-compact-bounded

Every compact operator is bounded.
```

```{dropdown} **Proof:**
The unit ball $B_1(0) \subset X$ is bounded, so by compactness of the operator, $\overline{K(B_1(0))}$
is compact and hence bounded in $Y$. Thus

$$
\sup_{\|x\| \leq 1} \|Kx\|_Y \leq M
$$

for some $M > 0$, which gives $\|K\|_{\mathrm{op}} \leq M$.
```

The converse is false in infinite dimensions: the identity operator $I : \ell^2 \to \ell^2$ is
bounded but not compact, since the orthonormal sequence $(e_n)$ is bounded but has no convergent
subsequence.

## The Space of Compact Operators

```{prf:proposition} Compact operators form a closed ideal
:label: prop-compact-ideal

Let $X, Y, Z$ be normed spaces with $Y$ a Banach space.

1. If $K : X \to Y$ is compact and $T : Y \to Z$ is bounded, then $TK$ is compact.
2. If $T : Z \to X$ is bounded and $K : X \to Y$ is compact, then $KT$ is compact.
3. The set $\mathcal{K}(X, Y)$ of compact operators is a **closed subspace** of $\mathcal{L}(X, Y)$
   in the operator norm.
```

In algebraic language, $\mathcal{K}(X, Y)$ is a **closed two-sided ideal** in $\mathcal{L}(X)$ when
$X = Y$. Composing a compact operator with any bounded operator (on either side) produces another
compact operator.

The closedness statement is the most important: it says that the operator-norm limit of compact
operators is again compact. This is the key tool for proving compactness of specific operators.

```{prf:theorem} Limits of compact operators are compact
:label: thm-compact-limit

Let $X$ be a normed space and $Y$ a Banach space. If $(K_n)$ is a sequence of compact operators
in $\mathcal{L}(X, Y)$ with $K_n \to K$ in the operator norm, then $K$ is compact.
```

````{dropdown} **Proof:**
Let $(x_j)$ be a bounded sequence in $X$. We use a **diagonal argument**.

Since $K_1$ is compact, $(K_1 x_j)$ has a convergent subsequence $K_1 x_{j}^{(1)}$.

Since $K_2$ is compact, $(K_2 x_j^{(1)})$ has a convergent subsequence $K_2 x_j^{(2)}$.

Continuing, at stage $l$ the sequence $(K_l x_j^{(l)})$ converges. The diagonal sequence
$y_j := x_j^{(j)}$ satisfies: $(K_l y_j)_j$ converges for every $l$.

Now estimate:

$$
\|K y_i - K y_j\| \leq \underbrace{\|K y_i - K_n y_i\|}_{\leq \|K - K_n\| \cdot C}
  + \underbrace{\|K_n y_i - K_n y_j\|}_{\to 0 \text{ as } i,j \to \infty}
  + \underbrace{\|K_n y_j - K y_j\|}_{\leq \|K - K_n\| \cdot C}
$$

where $C = \sup_j \|y_j\|$. For any $\varepsilon > 0$, first choose $n$ so that
$\|K - K_n\| < \varepsilon / 3C$, then choose $i, j$ large enough so that
$\|K_n y_i - K_n y_j\| < \varepsilon / 3$. Thus $(K y_j)$ is Cauchy in $Y$ and converges since $Y$
is a Banach space.
````

```{prf:corollary} K(X,Y) is a Banach space
:label: cor-compact-banach

The space $\mathcal{K}(X, Y)$ of compact operators from a normed space $X$ into a Banach space $Y$
is itself a Banach space.
```


## Finite-Rank Operators: Compact Operators as "Infinite-Dimensional Matrices"

The connection between compact operators and matrices runs through finite-rank operators.

```{prf:definition} Finite-rank operator
:label: def-finite-rank

A bounded linear operator $A : X \to Y$ has **finite rank** if its range $R(A)$ is
finite-dimensional. We write $\mathrm{rank}(A) = \dim R(A)$.
```

```{prf:proposition} Finite-rank operators are compact
:label: prop-finite-rank-compact

Every bounded operator with finite-dimensional range is compact.
```

```{dropdown} **Proof:**
Let $(x_n)$ be a bounded sequence in $X$. Then $(Ax_n)$ is a bounded sequence in the
finite-dimensional space $R(A)$. By Bolzano-Weierstrass, it has a convergent subsequence.
```

This is the precise sense in which compact operators generalize matrices. A matrix
$A \in \mathbb{R}^{m \times n}$ defines an operator of rank at most $\min(m, n)$—always finite.
The key theorem ({prf:ref}`thm-compact-limit`) now tells us:

> **Compact operators are precisely the operators that can be approximated by "matrices"
> (finite-rank operators) in the operator norm.**

In Hilbert spaces this is exact: every compact operator is the operator-norm limit of
finite-rank operators. In general Banach spaces, this is the **approximation property** (which
most natural spaces satisfy, though Enflo showed it can fail).

```{prf:remark}
:label: rem-compact-matrix-analogy

The analogy between compact operators and matrices is not just a slogan. Here is a dictionary:

| Finite dimensions ($\mathbb{R}^n \to \mathbb{R}^m$) | Compact operators ($X \to Y$) |
|------|------|
| Every operator has finite rank | Approximated by finite-rank operators |
| Spectrum = eigenvalues | Spectrum = eigenvalues $\cup\ \{0\}$ |
| Each eigenvalue has finite multiplicity | Each nonzero eigenvalue has finite multiplicity |
| SVD: $A = \sum_{i=1}^r \sigma_i u_i v_i^T$ | SVD: $K = \sum_{i=1}^\infty \sigma_i \langle \cdot, v_i \rangle \, u_i$ |
| Symmetric: $A = Q\Lambda Q^T$ | Self-adjoint: $K = \sum_{i=1}^\infty \lambda_i \langle \cdot, \psi_i \rangle \, \psi_i$ |
| Fredholm alternative holds | Fredholm alternative holds |

The SVD holds for **every** compact operator between Hilbert spaces. The eigenvalue decomposition
into an orthonormal eigenbasis requires the additional assumption that the operator is
**self-adjoint** (just as $A = Q\Lambda Q^T$ requires symmetry in finite dimensions). Without
self-adjointness, a compact operator's eigenvectors need not form a basis.

Everything that makes finite-dimensional linear algebra work carries over to compact operators.
What fails for general bounded operators in infinite dimensions is exactly what compact operators
restore.
```


## The Key Example: Integral Operators

Our main source of compact operators is integral operators with square-integrable kernels.

```{prf:theorem} Hilbert-Schmidt integral operators are compact
:label: thm-hs-compact

Let $\Omega \subset \mathbb{R}^d$ be bounded and let $k \in L^2(\Omega \times \Omega)$. Then the
integral operator

$$
Kf(x) := \int_\Omega k(x, y) f(y) \, dy
$$

defines a compact operator $K : L^2(\Omega) \to L^2(\Omega)$.
```

````{dropdown} **Proof:**
Choose an orthonormal basis $\{\varphi_j\}$ of $L^2(\Omega)$. Then
$\{\varphi_i(x) \varphi_j(y)\}$ is an ONB of $L^2(\Omega \times \Omega)$, so

$$
k(x, y) = \sum_{i,j=1}^{\infty} k_{ij} \, \varphi_i(x) \varphi_j(y), \qquad
\|k\|_{L^2(\Omega \times \Omega)}^2 = \sum_{i,j=1}^{\infty} |k_{ij}|^2.
$$

Define truncations $k_n(x,y) := \sum_{i,j=1}^{n} k_{ij} \, \varphi_i(x) \varphi_j(y)$ and
corresponding operators $K_n$. For $f = \sum_{l=1}^{\infty} c_l \varphi_l$:

$$
K_n f = \sum_{i,j=1}^{n} k_{ij} c_j \, \varphi_i(x).
$$

Each $K_n$ has finite-dimensional range (rank $\leq n$), hence is compact by
{prf:ref}`prop-finite-rank-compact`. The approximation error satisfies

$$
\|K - K_n\|^2 \leq \int_\Omega \int_\Omega |k(x,y) - k_n(x,y)|^2 \, dx \, dy
= \sum_{i,j=n+1}^{\infty} |k_{ij}|^2 \to 0.
$$

By {prf:ref}`thm-compact-limit`, $K$ is compact.
````

```{prf:remark}
:label: rem-hs-svd

The proof above is really a **finite-rank approximation** argument. The kernel $k(x,y)$ is expanded
in an ONB for $L^2(\Omega \times \Omega)$, and truncating to $n$ terms gives a rank-$n$ operator
that converges to $K$ in the operator norm. This is analogous to truncating the SVD of a matrix to
$r$ singular values to obtain a best rank-$r$ approximation (the Eckart-Young theorem). However, the
expansion here uses an *arbitrary* ONB, not the singular functions of $K$. The true SVD of the
integral operator would use the eigenbases of $K^*K$ and $KK^*$.
```


```{prf:example} The solution operator for Poisson's equation is compact
:label: ex-poisson-compact

Consider the Poisson equation on $[0, L]$ with Neumann boundary conditions:

$$
-u'' = f, \quad u'(0) = u'(L) = 0, \quad \int_0^L u(x) \, dx = M.
$$

Integrating twice and applying Fubini gives the solution

$$
u(x) = \int_0^L g(x, s) f(s) \, ds + c
$$

where $g$ is the Green's function (an $L^2$ kernel). The solution operator $A^{-1} : f \mapsto u$
is an integral operator with an $L^2$ kernel, hence compact by {prf:ref}`thm-hs-compact`.

This is a fundamental pattern: **differential operators are unbounded, but their inverses
(solution operators) are often compact.** The compactness of $A^{-1}$ is what gives the Laplacian
a discrete spectrum of eigenvalues.
```


```{prf:example} Non-example: unbounded operators are not compact
:label: ex-derivative-not-compact

The second derivative operator $A = -\frac{d^2}{dx^2} : D(A) \to L^2(0,1)$ is unbounded, and
therefore not compact. Compact operators are always bounded ({prf:ref}`prop-compact-bounded`).
```


## Spectral Theory of Compact Operators

The spectral theory of compact operators is the payoff: it tells us that compact operators have
a spectrum that looks just like the spectrum of a matrix, up to a possible accumulation point at
zero.

### The Fredholm Alternative

```{prf:theorem} Spectral Fredholm Alternative
:label: thm-spectral-fredholm

Let $A : H \to H$ be a compact linear operator on a Hilbert space $H$. Then:

1. The spectrum $\sigma(A)$ is a compact subset of $\mathbb{C}$ whose only possible accumulation
   point is $\lambda = 0$.
2. For each $\lambda \in \mathbb{C} \setminus \{0\}$, exactly one of the following holds:
   - **(Alternative 1):** $\lambda \in \rho(A)$, i.e., $(A - \lambda I)^{-1}$ exists and is bounded.
     The equation $Ax - \lambda x = y$ has a unique solution for every $y$.
   - **(Alternative 2):** $\lambda \in \sigma_p(A)$ is an eigenvalue of **finite multiplicity**.
     The equation $Ax - \lambda x = 0$ has a nontrivial finite-dimensional solution space.
```

```{prf:remark}
:label: rem-fredholm-significance

Compare this with finite dimensions: for a matrix $A \in \mathbb{R}^{n \times n}$ and $\lambda \neq 0$,
either $\det(A - \lambda I) \neq 0$ (invertible) or $\det(A - \lambda I) = 0$ (eigenvalue with
finite-dimensional eigenspace). The Fredholm alternative is exactly this dichotomy, extended to
infinite dimensions via compactness. Without compactness, the spectrum can contain continuous and
residual parts that have no finite-dimensional analogue.
```


### The Hilbert-Schmidt Theorem

When the compact operator is additionally self-adjoint, we get a complete spectral decomposition—the
infinite-dimensional analogue of the eigenvalue decomposition of a symmetric matrix.

```{prf:theorem} Hilbert-Schmidt Spectral Theorem
:label: thm-hilbert-schmidt

Let $A : H \to H$ be a linear, compact, and self-adjoint operator on a Hilbert space $H$. Then:

1. All eigenvalues $\lambda_i$ of $A$ are **real**.
2. Eigenvalues can accumulate only at $0$.
3. There exists an orthonormal set of eigenfunctions $\{\psi_i\}$ such that $A$ has the **spectral
   representation**

$$
A\varphi = \sum_{i=1}^{\infty} \lambda_i \langle \varphi, \psi_i \rangle \, \psi_i.
$$
```

This is the **infinite-dimensional eigendecomposition** for self-adjoint operators: the operator $A$
is completely determined by its eigenvalues and eigenfunctions, just as a symmetric matrix is
determined by its eigenvalues and eigenvectors. The spectral representation
$A = \sum \lambda_i \langle \cdot, \psi_i \rangle \psi_i$ is the direct analogue of the matrix
diagonalization $A = Q \Lambda Q^T$. Note that this is **not** the SVD—it is the eigenvalue
decomposition, which requires self-adjointness. The SVD
$K = \sum \sigma_i \langle \cdot, v_i \rangle u_i$ is a separate factorization that works for all
compact operators (see {prf:ref}`rem-compact-matrix-analogy`).

```{prf:remark}
:label: rem-fractional-powers

The spectral representation also provides a natural way to define **fractional powers** of operators.
If $A$ is a positive operator with $A\varphi = \sum \lambda_i \langle \varphi, \psi_i \rangle \psi_i$,
then we define

$$
A^\alpha \varphi := \sum_{i=1}^{\infty} \lambda_i^\alpha \langle \varphi, \psi_i \rangle \, \psi_i
$$

for $\alpha \geq 0$. This is used, for example, to define $\sqrt{-\Delta}$, which appears in the
study of fractional diffusion and Levy flights.
```


### Application: Spectral Theory of the Laplacian

```{prf:theorem} Spectral theorem for differential operators with compact inverse
:label: thm-spectral-laplacian

Let $A : D(A) \to H$ be a symmetric, linear, unbounded operator with $R(A) = H$, and suppose
$A^{-1}$ exists and is compact. Then:

1. There exists an infinite sequence of real eigenvalues $\{\lambda_n\}$ with
   $\lim_{n \to \infty} |\lambda_n| = +\infty$.
2. The eigenvectors $\{w_j\}$ can be chosen to form an orthonormal basis, and

$$
Au = \sum_{j=1}^{\infty} \lambda_j \langle u, w_j \rangle \, w_j.
$$
```

```{dropdown} **Connection to the Hilbert-Schmidt theorem:**
If $A^{-1}$ is compact and self-adjoint, then $A^{-1}$ satisfies the Hilbert-Schmidt theorem with
eigenvalues $\mu_j \to 0$. The eigenvalues of $A$ are $\lambda_j = 1/\mu_j \to \infty$.

This is the typical situation for Laplacian-type operators: $A = -\Delta$ with suitable boundary
conditions is unbounded, but the solution operator $A^{-1}$ (given by a Green's function) is
compact ({prf:ref}`ex-poisson-compact`). Hence $-\Delta$ has a discrete spectrum of eigenvalues
tending to infinity, with eigenfunctions forming an ONB. This is why Fourier series work:
the eigenfunctions of the Laplacian on $[0, 2\pi]$ are precisely $\{e^{inx}\}$.
```

## Looking Ahead

Compact operators are the bridge between the abstract operator theory of this chapter and several
later topics in the course:

- **Weak convergence + compact operator $\Rightarrow$ strong convergence.** If $x_n \rightharpoonup x$
  weakly and $K$ is compact, then $Kx_n \to Kx$ strongly. This is a key tool in the calculus of
  variations for passing to the limit in nonlinear problems.

- **Rellich-Kondrachov compactness.** The Sobolev embedding $H^1(\Omega) \hookrightarrow L^2(\Omega)$
  is compact for bounded $\Omega$. This is the source of compactness in elliptic PDE theory and the
  reason the direct method of the calculus of variations works.

- **Fixed point theory.** Compact operators are the setting for Schauder's fixed point theorem and
  the Leray-Schauder degree, which extend Brouwer's fixed point theorem to infinite dimensions.

