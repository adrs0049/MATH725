---
exports:
  - format: pdf
    template: plain_latex
    output: exports/exercises.pdf
    id: lops-exercises-pdf
downloads:
  - id: lops-exercises-pdf
    title: Download PDF
---

# Exercises

## Linear Operators

```{div} exercise

Let $X$ be a Banach space and $A : X \mapsto Y$ a bounded linear map. Show that

- The null-space is closed.
- If there exists $K > 0$ such that $||x|| \leq K ||Ax||$ then the range is closed.

```

## Banach-Steinhaus

```{div} exercise

Prove the above corollary. For (3) $\implies$ (2) pick a dense set $D \subset X$ and define $T(x) = \lim_{n} T_n(x)$
for $x\in D$. Then show that $T_n(x) \to T(x)$ for all $x \in X$.

```

```{div} exercise

Let $S \subset \mathcal{L}(X, Y)$ be a family of linear operators
such that $\sup_{T \in S} ||T|| < \infty$. Show that this means that $S$ is equi-continuous.

```

## Banach-Steinhaus Applications

```{div} exercise

**Divergence of Lagrange interpolation.**

Let $L_n$ be the Lagrange interpolation operator at Chebyshev nodes on $[-1,1]$.

1. Show that $\|L_n\| = \Lambda_n$ where $\Lambda_n$ is the Lebesgue constant.
2. Using $\Lambda_n \sim \frac{2}{\pi} \log n$, explain why Banach-Steinhaus does **not** give divergence.
3. Prove that for any $f \in C[-1,1]$, $\|f - L_n f\|_\infty \to 0$ (use Weierstrass + stability).
```

```{div} exercise

**Quadrature stability.**

Consider the midpoint rule $M_n f = \frac{1}{n} \sum_{k=1}^{n} f\left(\frac{2k-1}{2n}\right)$ on $[0,1]$.

1. Compute $\|M_n\|$.
2. Show that $M_n p \to \int_0^1 p$ for any polynomial.
3. Conclude that $M_n f \to \int_0^1 f$ for all $f \in C[0,1]$.
```

```{div} exercise

**Failure of pointwise convergence.**

Let $X = C[0,1]$ and define $T_n : X \to \mathbb{R}$ by $T_n f = n \int_0^{1/n} f(t) \, dt$.

1. Show each $T_n$ is bounded with $\|T_n\| = 1$.
2. Find $\lim_{n \to \infty} T_n f$ for continuous $f$.
3. This is an example where uniform boundedness holds and pointwise limits exist. What is the limit operator?
```

```{div} exercise

**Unbounded inverse.**

Let $X = \{f \in C^1[0,1] : f(0) = 0\}$ with norm $\|f\| = \|f'\|_\infty$, and $Y = C[0,1]$ with sup norm.

Define $T : X \to Y$ by $Tf = f$ (inclusion).

1. Show $T$ is bounded, linear, and bijective onto its range.
2. Compute $\|T^{-1}\|$ (the inverse is differentiation). Is it bounded?
3. Why doesn't this contradict Banach's bounded inverse theorem?
```

## Open Mapping Theorem

```{div} exercise
Show that all linear transformations from a finite-dimensional space to a
normed vector space are continuous. Conclude that all norms on a finite-dimensional
space are equivalent.

*Hint:* You can use either the open-mapping theorem or Banach-Steinhaus to prove this by considering
the identity map.

```

## Open Mapping Theorem Applications

```{div} exercise
**Condition number of differentiation.**

Consider $D : (C^1[0,1], \|\cdot\|_{C^1}) \to (C[0,1], \|\cdot\|_\infty)$ where $\|f\|_{C^1} = \|f\|_\infty + \|f'\|_\infty$.

1. Show $D$ is bounded with $\|D\| \leq 1$.
2. Find $\|D\|$ exactly.
3. Describe the "inverse" $D^{-1}$ (integration). On what domain is it defined?
4. Compute $\|D^{-1}\|$ and the condition number.
```

```{div} exercise
**Inf-sup for the divergence.**

Let $\Omega = (0,1)^2$, $V = H^1_0(\Omega)^2$, $Q = L^2_0(\Omega) = \{q : \int_\Omega q = 0\}$.

Define $b(\mathbf{v}, q) = \int_\Omega q \nabla \cdot \mathbf{v}$.

1. Show that $b$ is continuous.
2. The inf-sup condition states $\inf_{q} \sup_{\mathbf{v}} \frac{b(\mathbf{v},q)}{\|\mathbf{v}\|_{H^1}\|q\|_{L^2}} \geq \beta > 0$. Interpret this as an Open Mapping statement.
3. Why does this imply existence of $\mathbf{v} \in V$ with $\nabla \cdot \mathbf{v} = q$ and $\|\mathbf{v}\|_{H^1} \leq C\|q\|_{L^2}$?
```

```{div} exercise
**Closed Graph for integral operators.**

Let $K : L^2[0,1] \to L^2[0,1]$ be defined by $(Kf)(x) = \int_0^x f(t) dt$.

1. Prove $K$ has closed graph directly (without using continuity).
2. Show $K$ is bounded by computing $\|K\|$.
3. Is $K^{-1}$ bounded? (Consider the domain carefully.)
```

```{div} exercise
**Perturbation theory.**

Let $A : X \to X$ be invertible with $\|A^{-1}\| = M$.

1. Show that if $\|B\| < 1/M$, then $A + B$ is invertible.
2. Derive the bound $\|(A+B)^{-1} - A^{-1}\| \leq \frac{M^2 \|B\|}{1 - M\|B\|}$.
3. Apply this to $A = I$ to get the Neumann series.
```

## Compact Operators

```{div} exercise

Show that if $K : X \to Y$ is compact and $T : Y \to Z$ is bounded, then $TK$ is compact. Similarly,
show that if $T : Z \to X$ is bounded and $K : X \to Y$ is compact, then $KT$ is compact.

```

```{div} exercise

Let $H$ be a Hilbert space and $K : H \to H$ a compact operator. Show that if $(x_n)$ converges
weakly to $x$ (i.e. $\langle x_n, y \rangle \to \langle x, y \rangle$ for all $y \in H$), then
$Kx_n \to Kx$ in norm. That is, **compact operators map weakly convergent sequences to strongly
convergent sequences**.

*Hint:* Suppose for contradiction that $\|Kx_n - Kx\| \not\to 0$. Pass to a subsequence where
$\|Kx_{n_k} - Kx\| \geq \varepsilon$, then use compactness to extract a further subsequence where
$Kx_{n_{k_j}}$ converges. What must the limit be?

```

```{div} exercise

Let $K : L^2(0,1) \to L^2(0,1)$ be the integral operator

$$
Kf(x) = \int_0^1 \min(x, y) \, f(y) \, dy.
$$

1. Show that $K$ is compact by verifying that $k(x,y) = \min(x,y) \in L^2((0,1) \times (0,1))$.
2. Show that $K$ is self-adjoint: $\langle Kf, g \rangle = \langle f, Kg \rangle$.
3. Find the eigenvalues and eigenfunctions of $K$. *(Hint: differentiate $Kf = \lambda f$ twice to
   convert to an ODE.)*

```

```{div} exercise

Give an example of a bounded linear operator $T : \ell^2 \to \ell^2$ that is **not** compact. Prove
that your operator fails the sequential characterization of compactness.

```
