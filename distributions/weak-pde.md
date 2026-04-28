---
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/weak-pde.pdf
    id: distributions-weak-pde-pdf
downloads:
  - id: distributions-weak-pde-pdf
    title: Download PDF
---

# Application: Weak Formulation of PDEs

:::{tip} Big Idea
Fundamental solutions give explicit formulas but require constant
coefficients and no boundary. The weak formulation replaces the PDE with
an equation in a Sobolev dual space, reducing existence to the Riesz
representation theorem (symmetric case) or Lax-Milgram (general case).
The Gelfand triple $H^1_0 \hookrightarrow L^2 \hookrightarrow H^{-1}$
identifies where the solution, the data, and the bilinear form live.
:::


## From classical to weak solutions

Fundamental solutions give explicit formulas, but only for
constant-coefficient operators on all of $\mathbb{R}^d$. For bounded
domains with boundary conditions, or for variable-coefficient operators,
we need a different approach. Sobolev spaces provide it: instead of finding
a formula, we prove existence abstractly using duality.

The idea is to rewrite the PDE as a problem about functionals on a Hilbert
space. Consider $-\Delta u = f$ on a bounded domain $\Omega$ with $u = 0$
on $\partial\Omega$. The boundary condition is encoded by working in
$H^1_0(\Omega)$ (the closure of $C_c^\infty(\Omega)$ in $H^1$). Multiply
the PDE by a test function $v \in H^1_0(\Omega)$ and integrate by parts:

$$\int_\Omega \nabla u \cdot \nabla v\, dx = \int_\Omega f\, v\, dx \qquad \text{for all } v \in H^1_0(\Omega).$$

The boundary terms vanish because $v \in H^1_0$. This is the **weak
formulation**: find $u \in H^1_0(\Omega)$ satisfying the identity above.

### Existence by the Riesz representation theorem

**The PDE is an equation in the dual space.** The weak formulation is
not an equation between functions in $\Omega$; it is an equation between
*elements of $H^{-1}(\Omega) = H^1_0(\Omega)^*$*. Read both sides of
$(\text{weak})$ as functionals of the test direction $v$:

$$\underbrace{v \mapsto \int_\Omega \nabla u \cdot \nabla v\,dx}_{=:\,A u \;\in\; H^{-1}(\Omega)}
  \;=\;
  \underbrace{v \mapsto \int_\Omega f\,v\,dx}_{=:\,F \;\in\; H^{-1}(\Omega)}
  \qquad \text{in } H^{-1}(\Omega).$$

The left-hand functional $Au$ is continuous on $H^1_0$ by Cauchy-Schwarz
($|Au(v)| \leq \|\nabla u\|_{L^2}\|\nabla v\|_{L^2}$), so
$A : H^1_0 \to H^{-1}$ is a bounded operator. The right-hand functional $F$
is continuous on $H^1_0$ by Hölder plus Poincaré (for $f \in L^2$, or
more generally for $f \in H^{-1}$ by definition). Solving the PDE
means solving the linear equation $Au = F$ in $H^{-1}$.

This is the shift that distributions made possible. Classically
$-\Delta u = f$ is an equation between functions at each point
$x \in \Omega$; weakly, it is a single equation between two bounded
linear functionals on $H^1_0$. The equality is tested by pairing against
every $v \in H^1_0$, not by comparing pointwise values.

The left-hand side is simultaneously an inner product on $H^1_0(\Omega)$,
$\langle u, v \rangle_{\dot{H}^1} = \int \nabla u \cdot \nabla v\, dx$
(using the Poincaré inequality to show $\|\nabla \cdot\|_{L^2}$ is a norm
equivalent to $\|\cdot\|_{H^1}$ on $H^1_0$). That is what makes Riesz
applicable: the operator $A$ is the Riesz isomorphism
$H^1_0 \xrightarrow{\sim} H^{-1}$ associated with this inner product.

By the Riesz representation theorem ({prf:ref}`riesz-representation`),
there exists a unique $u_f \in H^1_0(\Omega)$ such that

$$\int_\Omega \nabla u_f \cdot \nabla v\, dx = f(v) \qquad \text{for all } v \in H^1_0(\Omega).$$

This $u_f$ is the weak solution. Existence and uniqueness are immediate
corollaries of a theorem we already proved in the duality chapter.

```{prf:remark}
:label: remark-riesz-pde
:class: dropdown

The Riesz map $(-\Delta)^{-1} : H^{-1}(\Omega) \to H^1_0(\Omega)$,
$f \mapsto u_f$, is the **inverse Laplacian**. It gains two derivatives:
the input $f$ lives in $H^{-1}$ (a distribution), but the output $u_f$
lives in $H^1$ (a function with a derivative in $L^2$).

This two-derivative gain is not a coincidence. If $f \in H^{-1}$, the
pairing $\langle f, v \rangle$ is defined abstractly. But the Riesz map
produces $u_f \in H^1_0$, and now

$$\langle f, v \rangle_{H^{-1} \times H^1} = \int_\Omega \nabla u_f \cdot \nabla v \, dx.$$

The singular object $f$ has been "absorbed" into $\nabla u_f \in L^2$. The
regularity of $u_f$ compensates exactly for the singularity of $f$.
```

### The Lax-Milgram theorem

The Riesz argument above works because the left-hand side
$\int \nabla u \cdot \nabla v\, dx$ *is* an inner product on $H^1_0$.
For more general operators (with lower-order terms, non-symmetric
coefficients, or convection) the bilinear form $B(u,v)$ may not be
symmetric, so it is not an inner product. The Lax-Milgram theorem handles
this case.

```{prf:theorem} Lax-Milgram
:label: lax-milgram

Let $V$ be a real Hilbert space. Suppose $B : V \times V \to \mathbb{R}$
is a bilinear form satisfying:

1. **Continuity**: $|B(u,v)| \leq M \|u\|_V \|v\|_V$ for all $u, v \in V$,
2. **Coercivity**: $B(u,u) \geq \alpha \|u\|_V^2$ for all $u \in V$,

for constants $M, \alpha > 0$. Then for every $f \in V^*$, there exists a
unique $u \in V$ such that

$$B(u,v) = \langle f, v \rangle \qquad \text{for all } v \in V,$$

and $\|u\|_V \leq \frac{1}{\alpha}\|f\|_{V^*}$.
```

```{prf:proof}
:class: dropdown

For each fixed $u \in V$, the map $v \mapsto B(u,v)$ is a continuous linear
functional on $V$ (by the continuity bound). By the Riesz representation
theorem, there exists a unique $Au \in V$ such that

$$B(u,v) = \langle Au, v \rangle_V \qquad \text{for all } v \in V.$$

This defines a linear operator $A : V \to V$. Continuity of $B$ gives
$\|Au\|_V \leq M\|u\|_V$. Coercivity gives

$$\alpha\|u\|_V^2 \leq B(u,u) = \langle Au, u \rangle_V \leq \|Au\|_V\|u\|_V,$$

so $\|Au\|_V \geq \alpha\|u\|_V$. This means $A$ is injective and has
closed range. To show surjectivity: if $w \perp \operatorname{range}(A)$,
then $0 = \langle Aw, w \rangle = B(w,w) \geq \alpha\|w\|^2$, so $w = 0$.
Hence $A$ is bijective.

Now represent $f$ via Riesz: there exists $\tilde{f} \in V$ with
$\langle f, v \rangle = \langle \tilde{f}, v \rangle_V$. Set $u = A^{-1}\tilde{f}$.
Then $B(u,v) = \langle Au, v \rangle_V = \langle \tilde{f}, v \rangle_V = \langle f, v \rangle$
for all $v$. The bound $\|u\|_V \leq \frac{1}{\alpha}\|f\|_{V^*}$ follows from coercivity.
```

```{prf:remark} Riesz as a special case
:label: remark-riesz-special-case
:class: dropdown

When $B(u,v) = \langle u, v \rangle_V$ is the inner product itself,
Lax-Milgram reduces to the Riesz representation theorem with $M = \alpha = 1$.
```

```{prf:remark} Lax-Milgram and the direct method
:label: remark-lax-milgram-direct-method
:class: dropdown

The two hypotheses of Lax-Milgram play exactly the same roles as the two
ingredients of the direct method for variational problems. Recall the
direct method ({prf:ref}`direct-method-dirichlet`): to minimize
$E: V \to \mathbb{R}$, take a minimizing sequence $u_n$, use *coercivity*
to force $(u_n)$ to be bounded, use *Banach-Alaoglu*
({prf:ref}`banach-alaoglu`) to extract a weakly convergent subsequence
$u_{n_k} \rightharpoonup u$, and use *weak lower semicontinuity* to
conclude $E(u) \leq \liminf E(u_{n_k}) = \inf E$. Two ingredients:
coercivity to *get* a weak limit, weak l.s.c. to *pass to it*.

When $B$ is symmetric, Lax-Milgram *is* the direct method applied to the
energy

$$E(v) = \tfrac{1}{2} B(v,v) - \langle f, v \rangle,$$

whose Euler-Lagrange equation is $B(u,v) = \langle f, v\rangle$. The two
Lax-Milgram hypotheses translate into the two direct-method ingredients
as follows.

**Coercivity of $B$ $\Longrightarrow$ coercivity of $E$.** From
$B(v,v) \geq \alpha\|v\|^2$,

$$E(v) \;\geq\; \tfrac{\alpha}{2}\|v\|^2 - \|f\|_{V^*}\|v\| \;\longrightarrow\; \infty
\quad \text{as } \|v\| \to \infty.$$

So minimizing sequences are bounded in $V$. This is the same mechanism
that produces the a priori estimate $\|u\|_V \leq \tfrac{1}{\alpha}\|f\|_{V^*}$
in the Lax-Milgram conclusion: coercivity controls the size of the
solution.

**Continuity of $B$ + symmetry + coercivity $\Longrightarrow$ weak
l.s.c. of $E$.** This step is subtler than it looks. Continuity of $B$
makes $v \mapsto \tfrac{1}{2} B(v,v)$ continuous in the *norm* topology
(since $|B(v,v)| \leq M\|v\|^2$), but norm continuity alone does **not**
imply weak l.s.c. — $v \mapsto -\|v\|^2$ is norm-continuous yet fails to
be weakly l.s.c. The bridge is **convexity**, supplied by
{prf:ref}`Mazur's theorem <mazur-theorem>`:

> A convex, norm-continuous functional on a Banach space is weakly
> lower semicontinuous.

Symmetry together with coercivity makes $v \mapsto \tfrac12 B(v,v)$ a
positive-definite quadratic form, hence convex. Continuity then promotes
convexity to weak l.s.c. via Mazur. So the honest reading of the
Lax-Milgram hypotheses under symmetry is

$$\underbrace{\text{continuity}}_{\text{norm continuity of } E}
\;+\;
\underbrace{\text{coercivity} + \text{symmetry}}_{\text{convexity of } E}
\;\xrightarrow{\text{Mazur}}\;
\text{weak l.s.c. of } E.$$

The shorthand "continuity of $B$ $\leftrightarrow$ weak l.s.c." is
harmless in the symmetric setting because convexity is already on the
table for free.

**Non-symmetric case.** When $B$ is not symmetric there is no energy to
minimize, and the direct method does not literally apply. The proof of
Lax-Milgram instead routes through Riesz representation and the operator
$A: V \to V$ with $B(u,v) = \langle Au, v\rangle_V$. But the *roles* of
the two hypotheses are preserved:

- Coercivity gives the lower bound $\|Au\|_V \geq \alpha \|u\|_V$, which
  forces $A$ to be injective with closed range — the "compactness /
  a priori bound" step.
- Continuity makes $A$ a bounded operator in the first place — the
  "pass to the limit" step.

So the dichotomy *coercivity controls size, continuity controls limits*
survives even when there is no energy functional in sight.
```

## The Gelfand triple

The natural framework for weak formulations is a triple of spaces

$$V \hookrightarrow H \hookrightarrow V^*$$

where $V$ is a Hilbert space (the "energy space"), $H$ is a pivot space,
and $V^*$ is the dual. The embeddings are continuous and dense.

The prototypical example is

$$H^1_0(\Omega) \hookrightarrow L^2(\Omega) \hookrightarrow H^{-1}(\Omega).$$

An element $f \in H^{-1}$ acts on test functions in $H^1_0$ via the
duality pairing. The PDE $Au = f$ is an equation *in $H^{-1}$*: we seek
$u \in H^1_0$ such that $B(u,v) = \langle f, v \rangle_{H^{-1} \times H^1_0}$
for all $v \in H^1_0$. The Gelfand triple identifies which space each
player lives in:

- The **solution** $u$ lives in the energy space $V = H^1_0$.
- The **data** $f$ lives in the dual $V^* = H^{-1}$.
- The **bilinear form** $B : V \times V \to \mathbb{R}$ connects them.
- The **pivot** $H = L^2$ sits in between, providing the $L^2$ inner
  product that mediates between function values and functionals.

```{prf:example} General second-order elliptic operator
:label: ex-general-elliptic

Consider the operator $Lu = -\operatorname{div}(A(x)\nabla u) + b(x) \cdot \nabla u + c(x)u$
on a bounded domain $\Omega$ with Dirichlet boundary conditions. The
weak formulation is: find $u \in H^1_0(\Omega)$ such that

$$B(u,v) = \int_\Omega \big[ A(x)\nabla u \cdot \nabla v + (b(x) \cdot \nabla u)\,v + c(x)\,u\,v \big]\, dx = \langle f, v \rangle$$

for all $v \in H^1_0(\Omega)$.

- **Continuity** of $B$ follows from $A \in L^\infty$, $b \in L^\infty$,
  $c \in L^\infty$, and Cauchy-Schwarz.
- **Coercivity** requires uniform ellipticity ($A(x)\xi \cdot \xi \geq
  \lambda|\xi|^2$) and suitable bounds on $b$ and $c$ (or add a large
  enough multiple of $u$ to absorb the lower-order terms via Poincaré).

By Lax-Milgram, there exists a unique weak solution $u \in H^1_0(\Omega)$.
```


### What Sobolev spaces provide

Compared to the fundamental solution approach, the weak formulation gains:

1. **Boundary conditions.** The space $H^1_0(\Omega)$ encodes $u = 0$ on
   $\partial\Omega$. No need to modify the fundamental solution.

2. **Variable coefficients.** Replace
   $\int \nabla u \cdot \nabla v$ by $\int A(x)\nabla u \cdot \nabla v$
   for a matrix-valued coefficient $A(x)$. As long as $A$ is uniformly
   elliptic, the same argument works (via Lax-Milgram instead of Riesz).

3. **Regularity from the Sobolev scale.** The solution $u_f$ lives in
   $H^1_0$. If $f$ is more regular ($f \in L^2$ rather than $H^{-1}$),
   elliptic regularity gives $u_f \in H^2$. The Sobolev scale tracks
   exactly how regular the solution is.

4. **Compactness.** The embedding $H^1_0(\Omega) \hookrightarrow
   L^2(\Omega)$ is compact (Rellich-Kondrachov), so the inverse Laplacian
   $(-\Delta)^{-1} : L^2 \to H^1_0 \hookrightarrow L^2$ is a compact
   operator. This gives eigenvalues, eigenfunctions, and the spectral
   theory from the linear operators chapter.

### Two approaches, one solution

On a bounded domain $\Omega$, both approaches produce the same answer.
The **Green's function** $G(x,y)$ is the fundamental solution modified to
satisfy boundary conditions: $-\Delta_x G(x,y) = \delta(x-y)$ with
$G = 0$ on $\partial\Omega$. The convolution formula becomes

$$u(x) = \int_\Omega G(x,y)\, f(y)\, dy,$$

and this $u$ is also the Riesz representative in $H^1_0(\Omega)$. The
fundamental solution gives the explicit kernel; the Sobolev approach gives
existence without needing to find it.


## Nonlinear PDE via Compactness

The Lax-Milgram theorem handles linear equations. For nonlinear problems,
we need a different strategy: approximate, extract limits, and pass to the
limit in the nonlinear terms. The tools are Banach-Alaoglu (weak
compactness), Rellich-Kondrachov (compact embedding), and Sobolev
embedding (controlling the nonlinearity). We illustrate with a model
problem that ties together the entire theory.

### The model problem

Consider the semilinear elliptic equation

$$-\Delta u + u^3 = f \qquad \text{in } \Omega, \qquad u = 0 \text{ on } \partial\Omega,$$

where $\Omega \subset \mathbb{R}^d$ ($d \leq 3$) is bounded with Lipschitz
boundary and $f \in H^{-1}(\Omega)$. The cubic nonlinearity $u^3$ models a
restoring force that grows with amplitude.

The **weak formulation** is: find $u \in H^1_0(\Omega)$ such that

$$\int_\Omega \nabla u \cdot \nabla v \, dx + \int_\Omega u^3 v \, dx = \langle f, v \rangle \qquad \text{for all } v \in H^1_0(\Omega).$$

The nonlinear term $\int u^3 v \, dx$ is well-defined when $d \leq 3$
because the Sobolev embedding $H^1_0(\Omega) \hookrightarrow L^6(\Omega)$
(for $d = 3$) gives $u^3 \in L^2$ and $u^3 v \in L^1$.

### Galerkin approximation

Choose finite-dimensional subspaces $V_n \subset H^1_0(\Omega)$ with
$\bigcup_n V_n$ dense in $H^1_0(\Omega)$ (e.g., the span of the first $n$
eigenfunctions of $-\Delta$). The **Galerkin problem** is: find
$u_n \in V_n$ such that

$$\int_\Omega \nabla u_n \cdot \nabla v \, dx + \int_\Omega u_n^3 v \, dx = \langle f, v \rangle \qquad \text{for all } v \in V_n.$$

This is a finite-dimensional system, so Brouwer's fixed point theorem
guarantees the existence of a Galerkin solution $u_n$.

### A priori bounds

Test with $v = u_n$ itself:

$$\|\nabla u_n\|_{L^2}^2 + \|u_n\|_{L^4}^4 = \langle f, u_n \rangle \leq \|f\|_{H^{-1}}\|u_n\|_{H^1}.$$

By the Poincaré inequality ({prf:ref}`poincare-inequality`),
$\|u_n\|_{H^1} \leq C\|\nabla u_n\|_{L^2}$, so

$$\|\nabla u_n\|_{L^2}^2 \leq \|f\|_{H^{-1}} \cdot C\|\nabla u_n\|_{L^2}.$$

Dividing: $\|\nabla u_n\|_{L^2} \leq C\|f\|_{H^{-1}}$. The sequence
$(u_n)$ is **bounded in $H^1_0(\Omega)$**, uniformly in $n$.

### Extracting the limit

The bounded sequence $(u_n)$ in the reflexive space $H^1_0(\Omega)$ has a
weakly convergent subsequence by the Banach-Alaoglu theorem
({prf:ref}`banach-alaoglu`):

$$u_n \rightharpoonup u \quad \text{in } H^1_0(\Omega).$$

Weak convergence alone is not enough to pass to the limit in the
nonlinear term $u_n^3$. The map $u \mapsto u^3$ is continuous (in the
strong topology), but *continuous is not the same as weakly continuous*:
continuity preserves *strong* limits, and weak convergence is in
general only preserved by **linear** bounded operators. Nonlinear maps
can destroy weak limits through oscillation. The textbook example is
squaring: $u_n(x) = \sin(nx)$ on $(0, 2\pi)$ satisfies $u_n
\rightharpoonup 0$ in $L^2$, but

$$u_n^2 = \tfrac{1}{2} - \tfrac{1}{2}\cos(2nx) \;\rightharpoonup\;
  \tfrac{1}{2} \;\neq\; 0 = u^2,$$

so $u \mapsto u^2$ is *not* weakly continuous. Cubing fails the same
way: $u_n = 1 + \sin(nx)$ has $u_n \rightharpoonup 1$ but $u_n^3
\rightharpoonup \tfrac{5}{2} \neq 1 = u^3$ (the cross term $3\sin^2(nx)
\rightharpoonup 3/2$ is what leaks out). So knowing only that
$u_n \rightharpoonup u$ in $H^1_0$ is not enough to conclude
$u_n^3 \to u^3$ in any sense; we need strong convergence.

The fix is to upgrade weak convergence to strong convergence in a space
where the nonlinearity *is* continuous, and this is exactly what
**Rellich-Kondrachov** provides: applying
{prf:ref}`compact-weak-to-strong` with $T$ the compact embedding
$\iota : H^1_0 \hookrightarrow L^p$ (compact) for $p < 6$ (taking
$d=3$, so the Sobolev critical exponent is $2^* = 6$) upgrades the
weak-$H^1_0$ convergence of the Galerkin sequence, along a further
subsequence, to:

$$u_n \to u \quad \text{strongly in } L^p(\Omega) \text{ for } p < 6.$$

In particular, $u_n \to u$ in $L^4(\Omega)$. This strong convergence gives:

$$u_n^3 \to u^3 \quad \text{in } L^{4/3}(\Omega)$$

(since $\|u_n^3 - u^3\|_{L^{4/3}} \leq C\|u_n - u\|_{L^4}(\|u_n\|_{L^4}^2 + \|u\|_{L^4}^2)$
by the algebraic identity $a^3 - b^3 = (a-b)(a^2 + ab + b^2)$).

### Passing to the limit

Fix a test direction $v \in H^1_0(\Omega)$ (not just $v \in V_m$) and
read each side of the Galerkin equation as a value of a functional on
$H^1_0$. For every $n$, the maps

$$\Phi_n \;:\; v \;\mapsto\; \int_\Omega \nabla u_n \cdot \nabla v\,dx
  + \int_\Omega u_n^3\,v\,dx, \qquad
  F \;:\; v \;\mapsto\; \langle f, v \rangle$$

are continuous linear functionals on $H^1_0$, i.e. elements of
$H^{-1}(\Omega)$. The linear piece is continuous by Cauchy-Schwarz; the
nonlinear piece is continuous because $u_n \in H^1_0 \hookrightarrow L^4$
implies $u_n^3 \in L^{4/3} \hookrightarrow H^{-1}$ (Sobolev embedding
dualized). So the Galerkin identity is the statement $\Phi_n = F$ in
$H^{-1}$, but *restricted* to test directions $v \in V_m$, i.e. tested
only against a dense subset.

We want to upgrade this to $\Phi = F$ in $H^{-1}$ for a single limit
object $\Phi$. Both pieces of $\Phi_n$ converge, pointwise in $v$, to
the corresponding pieces built from $u$:

- **Linear term.** $u_n \rightharpoonup u$ in $H^1_0$ is exactly the
  statement $\int \nabla u_n \cdot \nabla v\,dx \to \int \nabla u \cdot
  \nabla v\,dx$ for every $v \in H^1_0$ (weak convergence *is* pointwise
  convergence of the Riesz functionals).
- **Nonlinear term.** Rellich upgraded weak-$H^1_0$ to strong-$L^4$
  convergence, hence $u_n^3 \to u^3$ in $L^{4/3}$. This upgrades to
  convergence in $H^{-1}$ via the continuous embedding $L^{4/3}
  \hookrightarrow H^{-1}$: for any $g \in L^{4/3}$, Hölder and Sobolev
  give

  $$\Bigl|\int g\,v\,dx\Bigr|
    \leq \|g\|_{L^{4/3}}\,\|v\|_{L^4}
    \leq C\,\|g\|_{L^{4/3}}\,\|v\|_{H^1_0},$$

  so $g$ defines a bounded linear functional on $H^1_0$ with
  $\|g\|_{H^{-1}} \leq C \|g\|_{L^{4/3}}$. This is exactly the dual of
  Sobolev $H^1_0 \hookrightarrow L^4$. Pairing with any fixed $v \in
  H^1_0 \subset L^4$ then gives $\int u_n^3 v\,dx \to \int u^3 v\,dx$.

So $\Phi_n(v) \to \Phi(v)$ for every $v \in H^1_0$, where
$\Phi(v) = \int \nabla u \cdot \nabla v + \int u^3 v$. For each $v \in V_m$
(any $m$) the identity $\Phi_n(v) = F(v)$ holds eventually, so passing
$n \to \infty$ yields $\Phi(v) = F(v)$ on the dense set $\bigcup_m V_m$.
Continuity of $\Phi$ and $F$ on $H^1_0$ extends this to all
$v \in H^1_0$. The Galerkin equation has upgraded to the identity
$\Phi = F$ in $H^{-1}$, which is the weak form $-\Delta u + u^3 = f$ we
set out to solve.

### Linear vs. nonlinear: why compactness was needed

Compare with the purely linear problem $-\Delta u = f$ from the start of
the section. There, existence followed from Riesz representation alone:
weak convergence in $H^1_0$ was *already* enough to pass to the limit,
because the only operation applied to $u_n$ was the continuous linear
functional $v \mapsto \int \nabla u_n \cdot \nabla v$. Linear bounded
operators preserve weak convergence by definition, so weak subsequential
limits suffice and Rellich is never needed.

Nonlinearity changes this. The map $u \mapsto u^3$ is continuous but
*not weakly continuous*, so weak convergence of $u_n$ gives no
information about $u_n^3$. The fix is to upgrade weak convergence to
strong convergence in a space where the nonlinearity is continuous, and
this upgrade is precisely what a compact embedding provides. This is the
general shape of the direct method: for linear problems weak
compactness (Banach-Alaoglu, Riesz) is enough; for nonlinear problems
weak compactness must be combined with a compact embedding
(Rellich-Kondrachov) to tame the nonlinear term.

**Why multiplication is the hard operation.** The obstruction is
structural, and the Banach-algebra chapter already told us what it is:
multiplication is a *frequency-convolution* operation
($\widehat{uv} = \hat u * \hat v$), so squaring or cubing a function
*sums its frequencies*. Two modes at frequencies $n$ and $m$ produce a
mode at frequency $n+m$. High-frequency content in $u_n$ therefore
breeds even higher frequencies in $u_n^3$, so $u_n^3$ can be strictly
*worse behaved* than $u_n$, and may leave the Sobolev space that $u_n$
lived in. That is why Sobolev spaces fail to be Banach algebras below
the threshold $s > d/p$ ({prf:ref}`sobolev-banach-algebra`): squaring
moves you out of the space, because the squared spectrum escapes the
regularity bound. The compactness trick sidesteps the problem by
reducing the question to strong convergence in a concrete $L^q$, where
multiplication *is* continuous (Hölder), rather than working in the
$H^s$ where multiplication might blow up the regularity budget.


