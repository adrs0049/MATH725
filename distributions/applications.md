---
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/applications.pdf
    id: distributions-applications-pdf
downloads:
  - id: distributions-applications-pdf
    title: Download PDF
---

# Application: Differential Equations

:::{tip} Big Idea
A fundamental solution $E$ of a linear operator $L$ solves $LE = \delta$.
Once you have it, convolution $u = E * f$ solves $Lu = f$ for any source
$f$. This is the continuous analogue of the superposition principle from
ODEs: the integral replaces the sum, and $\delta$ replaces the basis
vectors.
:::

## From ODE Superposition to PDE Convolution

In ODEs, if $L$ is a linear operator and we can solve $Ly_i = f_i$ for
individual sources $f_i$, then linearity gives
$L(\sum c_i y_i) = \sum c_i f_i$. This is the superposition principle for
finite sums.

For PDEs, we replace the finite sum with an integral. Any source $f$ can
be decomposed as a continuous superposition of point sources:

$$f(x) = \int_{\mathbb{R}^d} f(y)\, \delta(x - y)\, dy.$$

This is just the sifting property of the delta, but read physically it says:
$f$ is a superposition of impulses $\delta(\cdot - y)$, each weighted by
$f(y)$. If $E$ is the response to a single impulse at the origin (i.e.
$LE = \delta$), then by translation $E(\cdot - y)$ is the response to an
impulse at $y$. Superposing all these responses:

$$u(x) = \int_{\mathbb{R}^d} f(y)\, E(x - y)\, dy = (E * f)(x).$$

Since $L$ acts on $x$ and the integral is over $y$, linearity gives

$$Lu(x) = \int_{\mathbb{R}^d} f(y)\, LE(x - y)\, dy = \int_{\mathbb{R}^d} f(y)\, \delta(x - y)\, dy = f(x).$$

So $u = E * f$ solves $Lu = f$. Convolution with the fundamental solution
*is* the superposition principle, generalized from sums to integrals.


## Fundamental Solutions

```{prf:definition} Fundamental solution
:label: def-fundamental-solution

Let $L = \sum_{|\alpha| \leq m} a_\alpha D^\alpha$ be a linear partial
differential operator with constant coefficients $a_\alpha \in \mathbb{R}$.
A **fundamental solution** of $L$ is a distribution
$E \in \mathcal{D}'(\mathbb{R}^d)$ satisfying

$$LE = \delta.$$
```

The equation $LE = \delta$ is understood in the distributional sense:
$\langle LE, \varphi \rangle = \langle \delta, \varphi \rangle = \varphi(0)$
for all $\varphi \in \mathcal{D}(\mathbb{R}^d)$. By the definition of
distributional differentiation, this becomes
$\langle E, L^*\varphi \rangle = \varphi(0)$, where $L^*$ is the formal
adjoint of $L$.

**Why distributions are essential here.** The equation $LE = \delta$ has
no meaning in classical analysis: the right-hand side is not a function.
But even the left-hand side is misleading classically. Consider the
Laplacian in $\mathbb{R}^3$: the function $E(x) = -1/(4\pi|x|)$ satisfies
$\Delta E(x) = 0$ for every $x \neq 0$. Pointwise, the Laplacian cannot
"see" the singularity at the origin. But as a distribution, $E$ acts on
test functions via integration, and the singularity contributes. When we
compute $\langle \Delta E, \varphi \rangle = \langle E, \Delta\varphi
\rangle$ and integrate by parts (excising a ball $B_\varepsilon(0)$,
applying Green's identity, taking $\varepsilon \to 0$), the boundary terms
on the small sphere do not vanish: they converge to $\varphi(0)$. That is
where the $\delta$ comes from. The distributional derivative detects a
contribution at the singularity that pointwise differentiation misses
entirely.

```{prf:example} Fundamental solution of the Laplacian
:label: ex-fundamental-laplacian
:class: dropdown

The Laplacian $\Delta = \sum_{i=1}^d \partial_i^2$ in $\mathbb{R}^d$ has
fundamental solution

$$E(x) = \begin{cases} \dfrac{1}{2}|x| & d = 1, \\[6pt] \dfrac{1}{2\pi}\log|x| & d = 2, \\[6pt] \dfrac{-1}{d(d-2)\omega_d}\,|x|^{2-d} & d \geq 3, \end{cases}$$

where $\omega_d$ is the volume of the unit ball in $\mathbb{R}^d$. In
three dimensions this gives the familiar $E(x) = -\frac{1}{4\pi|x|}$.

Each of these is locally integrable (the singularity at the origin is
integrable), so $E$ defines a regular distribution. The equation
$\Delta E = \delta$ can be verified by integration by parts: for any
$\varphi \in \mathcal{D}(\mathbb{R}^d)$,

$$\langle \Delta E, \varphi \rangle = \langle E, \Delta \varphi \rangle = \int_{\mathbb{R}^d} E(x)\,\Delta\varphi(x)\, dx = \varphi(0).$$

The last equality uses Green's second identity on the domain
$\{|x| > \varepsilon\}$ and a careful limit $\varepsilon \to 0$.
```

```{prf:example} Fundamental solution of the heat operator
:label: ex-fundamental-heat
:class: dropdown

The heat operator $L = \partial_t - \Delta$ in
$\mathbb{R}^d \times (0, \infty)$ has fundamental solution

$$E(x, t) = \frac{1}{(4\pi t)^{d/2}}\, e^{-|x|^2/4t}\, H(t),$$

where $H(t)$ is the Heaviside function. This is the **heat kernel**: a
Gaussian that spreads over time. For any bounded continuous initial
condition $f$, the convolution

$$u(x,t) = (E(\cdot, t) * f)(x) = \int_{\mathbb{R}^d} \frac{1}{(4\pi t)^{d/2}}\, e^{-|x-y|^2/4t}\, f(y)\, dy$$

solves the initial value problem $\partial_t u - \Delta u = 0$,
$u(\cdot, 0) = f$.
```


## The Malgrange-Ehrenpreis Theorem

A natural question: does every linear constant-coefficient operator have a
fundamental solution? The answer is yes.

```{prf:theorem} Malgrange-Ehrenpreis
:label: thm-malgrange-ehrenpreis

Every non-zero linear partial differential operator with constant
coefficients

$$L = \sum_{|\alpha| \leq m} a_\alpha D^\alpha, \qquad a_\alpha \in \mathbb{R},$$

has a fundamental solution $E \in \mathcal{D}'(\mathbb{R}^d)$.
```

This is a deep existence result, due independently to Malgrange and
Ehrenpreis in the 1950s.

```{prf:proof}
:class: dropdown

**(Sketch via Hahn-Banach.)** We need a distribution $E$ satisfying
$\langle E, L^*\varphi \rangle = \varphi(0)$ for all
$\varphi \in \mathcal{D}(\mathbb{R}^d)$. Define the linear functional

$$\Phi : L^*\big(\mathcal{D}(\mathbb{R}^d)\big) \to \mathbb{R}, \qquad \Phi(L^*\varphi) = \varphi(0).$$

This is well-defined on the image of $L^*$ (one must verify that
$L^*\varphi = 0$ implies $\varphi(0) = 0$, which is the hardest part of
the proof and requires estimates on $L^*$). The key analytic step is
showing that $\Phi$ is continuous with respect to the topology inherited
from $\mathcal{D}(\mathbb{R}^d)$: there exist a compact set $K$ and
constants $C, k$ such that

$$|\varphi(0)| \leq C \|L^*\varphi\|_{C^k(K)} \qquad \text{for all } \varphi \in \mathcal{D}(\mathbb{R}^d).$$

This estimate is the heart of the proof. Once it is established, the
Hahn-Banach theorem extends $\Phi$ to a continuous linear functional
$E$ on all of $\mathcal{D}(\mathbb{R}^d)$. This $E$ is a distribution
satisfying $LE = \delta$.
```

### Structure of the general solution

The fundamental solution $E$ is a **particular solution** of $Lu = \delta$,
just as in ODE theory. The general solution has the familiar form:
general = homogeneous + particular.

```{prf:proposition} General solution structure
:label: prop-general-solution

Let $L$ be a constant-coefficient operator.

1. **Non-uniqueness of fundamental solutions.** If $E$ is a fundamental
   solution of $L$ and $w \in \mathcal{D}'(\mathbb{R}^d)$ satisfies
   $Lw = 0$, then $E + w$ is also a fundamental solution.

2. **All fundamental solutions differ by homogeneous solutions.** If
   $E_1$ and $E_2$ are both fundamental solutions ($LE_1 = LE_2 = \delta$),
   then $L(E_1 - E_2) = 0$, so $E_1 - E_2$ is a solution of the
   homogeneous equation.

3. **General solution of $Lu = f$.** If $u_p = E * f$ is a particular
   solution of $Lu = f$, then every distributional solution of $Lu = f$ has
   the form $u = u_p + w$ where $Lw = 0$.
```

```{prf:proof}
:class: dropdown

Parts 1 and 2 follow from linearity: $L(E + w) = LE + Lw = \delta + 0 =
\delta$, and $L(E_1 - E_2) = LE_1 - LE_2 = \delta - \delta = 0$.

For part 3, if $Lu = f$ and $Lu_p = f$, then $L(u - u_p) = 0$, so
$w = u - u_p$ solves the homogeneous equation.
```

This is the exact analogue of the ODE theorem: the general solution of a
nonhomogeneous linear equation is a particular solution plus the general
solution of the homogeneous equation. Distribution theory provides the
particular solution via convolution; the homogeneous solutions depend on
the specific operator $L$ and on boundary or initial conditions.


## Solving PDEs via Convolution

With a fundamental solution in hand, the superposition argument from the
beginning of this section becomes rigorous.

```{prf:theorem} Solution by convolution
:label: thm-solution-convolution

Let $L$ be a constant-coefficient operator with fundamental solution $E$.
If $f \in \mathcal{D}(\mathbb{R}^d)$ (or more generally, if $f$ has
compact support and the convolution $E * f$ is well-defined), then

$$u = E * f$$

solves $Lu = f$ in $\mathcal{D}'(\mathbb{R}^d)$.
```

```{prf:proof}
:class: dropdown

By the properties of convolution and distributional differentiation:

$$Lu = L(E * f) = (LE) * f = \delta * f = f,$$

where we used that $L$ commutes with convolution (since $L$ has constant
coefficients), $LE = \delta$, and $\delta * f = f$ (the delta is the
identity for convolution).
```

This is the distributional realization of the superposition principle: each
point $y$ contributes an impulse response $f(y)\, E(\cdot - y)$, and the
integral over all $y$ assembles the solution.

```{prf:example} Solving Poisson's equation
:label: ex-poisson
:class: dropdown

Poisson's equation $-\Delta u = f$ in $\mathbb{R}^3$ has the solution

$$u(x) = (E * f)(x) = \frac{1}{4\pi} \int_{\mathbb{R}^3} \frac{f(y)}{|x - y|}\, dy,$$

which is the **Newton potential** of $f$. This is the gravitational (or
electrostatic) potential generated by a mass (or charge) density $f$.
```



