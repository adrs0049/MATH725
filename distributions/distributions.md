---
kernelspec:
  name: python3
  display_name: Python 3
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/distributions.pdf
    id: distributions-distributions-pdf
downloads:
  - id: distributions-distributions-pdf
    title: Download PDF
---

# Distributions as Functionals

With the inductive limit topology on $\mathcal{D}(\Omega)$ in hand, we can
now define distributions and equip them with a topology.

## Definition of Distributions

```{prf:definition} Distributions
:label: def-distributions

A **distribution** on $\Omega$ is a continuous linear functional
$T : \mathcal{D}(\Omega) \to \mathbb{R}$. The space of all distributions is

$$\mathcal{D}'(\Omega) = \big(\mathcal{D}(\Omega)\big)^*,$$

the topological dual of $\mathcal{D}(\Omega)$. We write $\langle T, \varphi
\rangle = T(\varphi)$ for the pairing.
```

By {prf:ref}`prop-continuity-estimate`, $T$ is a distribution if and only if
for every compact $K \subset \Omega$, there exist $C > 0$ and $k \geq 0$
such that $|T(\varphi)| \leq C \|\varphi\|_{C^k(K)}$ for all $\varphi \in
\mathcal{D}_K(\Omega)$.

**Physical interpretation.** No physical measurement captures a true point
value. A thermometer averages molecular kinetic energy over a small volume.
An electric field probe averages over the test charge's spatial extent.
Position measurements in quantum mechanics are limited by the uncertainty
principle. The pairing $\langle T, \varphi \rangle$ captures this: the test
function $\varphi$ is the sensitivity profile of a measurement device, with
$\operatorname{supp}(\varphi)$ as the detection region and the shape of
$\varphi$ encoding how strongly each point contributes to the reading.
A distribution $T$ is then an object that can only be "observed" through
such averaged measurements, never through point evaluation. This is not a
limitation but a feature: it is precisely why distributions can accommodate
objects like the Dirac delta that have no pointwise values.

## Convergence of Distributions

```{prf:definition} Weak-$*$ topology on distributions
:label: def-weak-star-distributions

The **weak-$*$ topology** on $\mathcal{D}'(\Omega)$ is the coarsest
topology making every evaluation functional
$\Phi_\varphi(T) = \langle T, \varphi \rangle$ continuous. A sequence of
distributions $T_n$ converges to $T$ in this topology if and only if

$$\langle T_n, \varphi \rangle \to \langle T, \varphi \rangle \quad \text{for all } \varphi \in \mathcal{D}(\Omega).$$
```

This is **convergence in the sense of distributions**, one of the weakest
convergence notions in analysis. Yet limits are unique: the topology is
**Hausdorff** because if $T_1 \neq T_2$, there exists $\varphi$ with
$\langle T_1, \varphi \rangle \neq \langle T_2, \varphi \rangle$.

```{prf:remark}
:label: remark-topology-parallel
:class: dropdown

The parallel with Banach space duality is exact:

| Banach space setting | Distribution setting |
|---|---|
| Banach space $X$ | Test functions $\mathcal{D}(\Omega)$ |
| Dual space $X^*$ | Distributions $\mathcal{D}'(\Omega)$ |
| Norm topology on $X$ | Inductive limit topology on $\mathcal{D}(\Omega)$ |
| Weak-$*$ topology on $X^*$ | Standard topology on $\mathcal{D}'(\Omega)$ |
| $f(x)$ for $f \in X^*, x \in X$ | $\langle T, \varphi \rangle$ for $T \in \mathcal{D}', \varphi \in \mathcal{D}$ |
| Weak-$*$ convergence: $f_n(x) \to f(x)$ | Distributional convergence: $T_n(\varphi) \to T(\varphi)$ |
| Banach–Alaoglu: closed balls are weak-$*$ compact | Distributions are weak-$*$ sequentially complete |

The key difference is that $\mathcal{D}(\Omega)$ is **not** a Banach space,
so results like Banach–Alaoglu do not apply directly. Compactness and
completeness results for distributions rely on the specific structure of the
inductive limit. But the *language* and *intuition* transfer directly from
the duality chapter.
```


## The Hierarchy of Distributions

The examples below are organized by the inclusion chain

$$
C(\Omega) \subset L^1_{\mathrm{loc}}(\Omega) \subset \mathcal{M}(\Omega) \subset \mathcal{D}'(\Omega),
$$

with each level strictly enlarging the previous one. To understand *why*
each inclusion is strict, we introduce a unified probe: **concentrating
test functions**. Fix a point $x_0$ and a non-negative test function
$\varphi$ with $\int \varphi = 1$, and define

$$\varphi_n(x) = n^d\, \varphi(n(x - x_0)).$$

Then $\int \varphi_n = 1$ and
$\operatorname{supp}(\varphi_n) \to \{x_0\}$. In the physical picture,
$\varphi_n$ is a measurement device focusing on $x_0$. The growth rate of
$\langle T, \varphi_n \rangle$ as $n \to \infty$ is the signature that
separates the levels.

### Continuous functions: $C(\Omega) \hookrightarrow \mathcal{D}'$

A continuous function $f$ defines a distribution $T_f$ by integration.
Probing with concentrating test functions recovers the point value:

$$\langle T_f, \varphi_n \rangle = \int f(x)\, \varphi_n(x)\, dx \to f(x_0)$$

since $\varphi_n$ concentrates at $x_0$ and $f$ is continuous there. The
response is **bounded**.

### Regular distributions: $L^1_{\mathrm{loc}} \hookrightarrow \mathcal{D}'$

```{prf:definition} Regular distributions
:label: def-regular-distributions

A function $f \in L^1_{\mathrm{loc}}(\Omega)$ defines a distribution $T_f$
by

$$\langle T_f, \varphi \rangle = \int_\Omega f(x)\,\varphi(x)\,dx \qquad \text{for all } \varphi \in \mathcal{D}(\Omega).$$

Distributions of this form are called **regular**.
```

The map $f \mapsto T_f$ is injective (two functions that agree a.e. define
the same distribution), so we often identify $f$ with $T_f$ and write
$\langle f, \varphi \rangle$. Any measure absolutely continuous with
respect to Lebesgue measure is representable by a locally integrable
function, so regular distributions are exactly those generated by absolutely
continuous measures. The embedding $f \mapsto T_f$ gives an injection
$L^1_{\mathrm{loc}}(\Omega) \hookrightarrow \mathcal{D}'(\Omega)$.

```{prf:example} Regular distributions
:label: ex-regular-distributions
:class: dropdown

1. Any $f \in L^p(\Omega)$ with $1 \leq p \leq \infty$ is locally
   integrable, hence defines a regular distribution.

2. The **Heaviside function** $H(x) = \mathbf{1}_{[0,\infty)}(x)$ is in
   $L^1_{\mathrm{loc}}(\mathbb{R})$, so $\langle H, \varphi \rangle =
   \int_0^\infty \varphi(x)\, dx$ defines a regular distribution.

3. The **sign function** $\operatorname{sgn}(x)$ is in
   $L^1_{\mathrm{loc}}(\mathbb{R})$ but not continuous. It defines a
   regular distribution of order 0.
```

**Probing.** For $f \in L^1_{\mathrm{loc}}$, the response
$\langle T_f, \varphi_n \rangle \to f(x_0)$ at every **Lebesgue point**
$x_0$ of $f$ (almost everywhere). The response is still **bounded**,
just as for continuous functions. The inclusion
$C(\Omega) \subset L^1_{\mathrm{loc}}(\Omega)$ is strict (the Heaviside
function is locally integrable but not continuous), but both levels produce
bounded responses.

### Distributions from measures: $\mathcal{M} \hookrightarrow \mathcal{D}'$

```{prf:definition} Distributions from measures
:label: def-distributions-measures

Any Radon measure $\mu$ on $\Omega$ defines a distribution $T_\mu$ by

$$\langle T_\mu, \varphi \rangle = \int_\Omega \varphi(x) \, \mathrm{d}\mu(x).$$
```

This generalizes regular distributions: $T_f = T_{\mu_f}$ where
$\mu_f = f(x)\,\mathrm{d}x$. The class of Radon measures also includes
singular measures, so $\mu = \mu_{\mathrm{ac}} + \mu_{\mathrm{sing}}$. The
singular part includes point masses and more exotic objects such as the
Cantor measure. The embedding $\mu \mapsto T_\mu$ gives an injection
$\mathcal{M}(\Omega) \hookrightarrow \mathcal{D}'(\Omega)$.

```{prf:example} Dirac delta distribution
:label: ex-dirac-delta

For any $x_0 \in \Omega$, the **Dirac delta distribution** $\delta_{x_0}$
is defined by

$$\langle \delta_{x_0}, \varphi \rangle = \varphi(x_0).$$
```

This has order 0, since $|\langle \delta_{x_0}, \varphi \rangle| =
|\varphi(x_0)| \leq \|\varphi\|_{C^0(K)}$. The Dirac delta is a singular
distribution: it is a Radon measure (a point mass) but not representable
by any locally integrable function. So
$\delta_{x_0} \in \mathcal{M}(\Omega) \subset \mathcal{D}'(\Omega)$ but
$\delta_{x_0} \notin L^1_{\mathrm{loc}}(\Omega)$. This shows that the
inclusion $L^1_{\mathrm{loc}} \subset \mathcal{M}$ is strict.

**Probing.** For $\delta_{x_0}$:
$\langle \delta_{x_0}, \varphi_n \rangle = \varphi_n(x_0) = n^d\,
\varphi(0)$. The response grows as $\mathcal{O}(n^d)$. More generally, if
$\mu$ has a point mass of size $c$ at $x_0$, then $\langle T_\mu,
\varphi_n \rangle \sim c\, n^d$. This blowup is the signature of a
singular measure: no locally integrable function can produce
$\mathcal{O}(n^d)$ growth, because $\int f\, \varphi_n \to f(x_0)$ stays
bounded.

```{prf:remark} Physical space embeds into distribution space
:label: remark-Rd-embed-distributions
:class: dropdown

The map $x \mapsto \delta_x$ embeds $\mathbb{R}^d$ into
$\mathcal{D}'(\mathbb{R}^d)$. This embedding is:

- **Injective**: if $x \neq y$, choose $\varphi$ with $\varphi(x) = 1$
  and $\varphi(y) = 0$; then
  $\langle \delta_x, \varphi \rangle \neq \langle \delta_y, \varphi \rangle$.
- **Continuous**: if $x_n \to x$ in $\mathbb{R}^d$, then
  $\langle \delta_{x_n}, \varphi \rangle = \varphi(x_n) \to \varphi(x) =
  \langle \delta_x, \varphi \rangle$ for every test function $\varphi$, so
  $\delta_{x_n} \to \delta_x$ in $\mathcal{D}'$.
- **A homeomorphism onto its image**: the weak-$*$ topology restricted to
  $\{\delta_x : x \in \mathbb{R}^d\}$ recovers the Euclidean topology,
  because test functions separate points of $\mathbb{R}^d$.
- **Closed**: the image $\{\delta_x : x \in \mathbb{R}^d\}$ is a closed
  subset of $\mathcal{D}'$. If $\delta_{x_n} \to T$ in $\mathcal{D}'$
  and $x_n \to \infty$, then $\langle T, \varphi \rangle = 0$ for every
  test function (since eventually $x_n \notin \operatorname{supp}(\varphi)$),
  so $T = 0$, which is not a $\delta_x$. Any convergent subsequence
  must have $x_n$ bounded, hence convergent, so $T = \delta_{x_\infty}$.

Physical space $\mathbb{R}^d$ thus sits inside $\mathcal{D}'(\mathbb{R}^d)$
as a closed $d$-dimensional submanifold. The passage from classical to
distributional analysis replaces "a function assigns values to points"
with "a distribution assigns values to test functions." The points
themselves are still present, embedded as the simplest distributions.
```

### Distributions beyond measures: $\mathcal{D}' \setminus \mathcal{M}$

The full power of distribution theory appears at this level: objects that
cannot be represented by any measure. A Radon measure $\mu$ acts on a
function through integration, so its action depends only on the *values*
of the function, controlled by

$$|\langle \mu, \varphi \rangle| = \left|\int \varphi\, d\mu\right| \leq |\mu|(\operatorname{supp} \varphi) \cdot \sup|\varphi|.$$

The right-hand side involves only $\sup|\varphi|$, never any derivatives.
A distribution that "sees" derivatives of test functions cannot be a
measure.

```{prf:example} Derivative of the Dirac delta
:label: ex-delta-prime

The derivative $\delta'$ is defined by

$$\langle \delta', \varphi \rangle = -\varphi'(0).$$

More generally, for any multi-index $\alpha$:

$$\langle D^\alpha \delta, \varphi \rangle = (-1)^{|\alpha|} D^\alpha \varphi(0).$$
```

The distribution $D^\alpha \delta$ has order $|\alpha|$. The action of
$\delta'$ depends on the derivative $\varphi'(0)$, and no bound of the
form $|\varphi'(0)| \leq C \sup|\varphi|$ can hold: take
$\varphi_n(x) = \frac{1}{n}\psi(nx)$ for a fixed bump function $\psi$ with
$\psi'(0) = 1$, then $\sup|\varphi_n| \to 0$ but $\varphi_n'(0) = 1$.
So no measure can reproduce $\delta'$, and
$\delta' \in \mathcal{D}'(\Omega) \setminus \mathcal{M}(\Omega)$.
This shows that the inclusion $\mathcal{M} \subset \mathcal{D}'$ is strict.

```{prf:example} Principal value of $1/x$
:label: ex-principal-value

The distribution $\mathrm{p.v.}\,\frac{1}{x}$ is defined by

$$\left\langle \mathrm{p.v.}\,\frac{1}{x},\, \varphi \right\rangle = \lim_{\varepsilon \to 0} \int_{|x| > \varepsilon} \frac{\varphi(x)}{x}\, dx.$$
```

This limit exists for every $\varphi \in \mathcal{D}(\mathbb{R})$ because
the odd part of the integrand cancels the singularity at the origin. The
principal value is not a regular distribution ($1/x$ is not locally
integrable), but it is also not a measure. The same scaling argument
applies: take $\varphi_n(x) = \frac{1}{n}\psi(nx)$ where $\psi$ is an odd
bump with $\int \psi(x)/x\, dx = c \neq 0$. Then $\sup|\varphi_n| \to 0$,
but by the substitution $u = nx$,

$$\left\langle \mathrm{p.v.}\,\frac{1}{x},\, \varphi_n \right\rangle = \int \frac{\psi(u)}{u}\, du = c \neq 0.$$

So no order-0 estimate holds, and
$\mathrm{p.v.}\,\frac{1}{x} \in \mathcal{D}'(\mathbb{R}) \setminus
\mathcal{M}(\mathbb{R})$.

**Probing.** For a distribution of order $m$, the response grows as
$\langle T, \varphi_n \rangle = \mathcal{O}(n^m)$. For $\delta'$:
$\langle \delta', \varphi_n \rangle = -\varphi_n'(0) =
-n^{d+1}\varphi'(0)$, giving growth of order $n^{d+1}$. Measures (order 0)
produce at most $\mathcal{O}(n^d)$ growth, so the faster rate is the
quantitative reason $\delta'$ cannot be a measure.

### The growth rate as a signature

The concentrating probe $\varphi_n$ acts as a diagnostic: bounded response
means a function, $\mathcal{O}(n^d)$ growth means a singular measure, and
$\mathcal{O}(n^m)$ growth for $m > d$ means a distribution that is not a
measure. This connects back to {prf:ref}`prop-separation`: test functions
separate distributions because different distributions respond differently
to these probes. The concentrating sequence is the concrete mechanism by
which test functions "see" the difference between a function, a measure,
and a genuinely distributional object.


## Topological Properties of $\mathcal{D}'(\Omega)$

With the examples in hand, we return to the topology of $\mathcal{D}'(\Omega)$
and establish the structural results that make distribution theory work:
separation, completeness, density, and the remarkable collapse of the
weak-$*$ and strong topologies.

### Separation

The weak-$*$ topology is Hausdorff: test functions separate distributions.
The converse (that distributions separate test functions) is less obvious
and requires the Hahn-Banach theorem.

```{prf:proposition} Distributions separate test functions
:label: prop-separation

If $\varphi_1 \neq \varphi_2$ in $\mathcal{D}(\Omega)$, there exists a
distribution $T \in \mathcal{D}'(\Omega)$ such that $\langle T, \varphi_1
\rangle \neq \langle T, \varphi_2 \rangle$.
```

```{prf:proof}
:class: dropdown

The version of Hahn-Banach from the duality chapter assumes a normed space,
and $\mathcal{D}(\Omega)$ is not normed. What applies here is the
**geometric Hahn-Banach theorem** (the separation theorem), which holds on
any **locally convex** topological vector space. Since
$\mathcal{D}(\Omega)$ is an inductive limit of Fréchet spaces, it is
locally convex, and the theorem guarantees a continuous linear functional
separating $\varphi_1$ from $\varphi_2$.
```

### Sequential completeness

```{prf:proposition} Sequential completeness
:label: prop-sequential-completeness

Every weak-$*$ Cauchy sequence in $\mathcal{D}'(\Omega)$ converges to a
distribution. That is, if $\langle T_n, \varphi \rangle$ converges for
every $\varphi \in \mathcal{D}(\Omega)$, then the limit
$T(\varphi) = \lim_n \langle T_n, \varphi \rangle$ defines a distribution
$T \in \mathcal{D}'(\Omega)$.
```

```{prf:proof}
:class: dropdown

The map $T : \mathcal{D}(\Omega) \to \mathbb{R}$ defined by
$T(\varphi) = \lim_n T_n(\varphi)$ is linear (limits preserve linearity).
It remains to show continuity. Fix a compact $K \subset \Omega$. The
restrictions $T_n|_{\mathcal{D}_K}$ are a pointwise bounded family of
continuous linear functionals on the Fréchet space $\mathcal{D}_K$. By
Banach-Steinhaus, they are equicontinuous: there exist $C_K > 0$ and
$k_K \geq 0$ such that $|T_n(\varphi)| \leq C_K \|\varphi\|_{K,k_K}$ for
all $n$ and all $\varphi \in \mathcal{D}_K$. Passing to the limit,
$|T(\varphi)| \leq C_K \|\varphi\|_{K,k_K}$, so $T$ is continuous on each
$\mathcal{D}_K$, hence on $\mathcal{D}(\Omega)$.
```

### Sequential density

```{prf:proposition} Sequential density
:label: prop-sequential-density

Every distribution is the weak-$*$ limit of a sequence of test functions.
That is, for every $T \in \mathcal{D}'(\Omega)$, there exists a sequence
$\{\psi_n\} \subset \mathcal{D}(\Omega)$ such that $\langle T, \varphi
\rangle = \lim_n \int \psi_n \varphi\, dx$ for all
$\varphi \in \mathcal{D}(\Omega)$.
```

As a concrete instance: if $\{\rho_n\}$ is an approximation to the
identity (non-negative, $\int \rho_n = 1$, support shrinking to $\{0\}$),
then $\rho_n \to \delta$ in the sense of distributions, since

$$
\langle \rho_n, \varphi \rangle = \int \rho_n(x)\,\varphi(x)\,dx \to \varphi(0) = \langle \delta, \varphi \rangle
$$

for every test function $\varphi$.

### The Montel property: weak-$*$ equals strong

```{prf:remark} The Montel property
:label: remark-montel
:class: dropdown

A **Montel space** is a locally convex topological vector space in which
every bounded closed subset is compact. This is an
infinite-dimensional analogue of the Heine-Borel theorem: in
$\mathbb{R}^n$, bounded closed sets are compact, but in an
infinite-dimensional Banach space they never are (by Riesz's lemma, the
closed unit ball is not compact). Montel spaces recover this compactness
despite being infinite-dimensional.

**Why $\mathcal{D}_K$ is Montel.** A bounded set in $\mathcal{D}_K$ is one
where all seminorms $\|\cdot\|_{K,k}$ are uniformly bounded, i.e. all
derivatives up to every order are uniformly bounded on $K$. By the
Arzelà-Ascoli theorem, uniform boundedness of a family of functions and
their first derivatives on a compact set implies a subsequence converging
in $C^0(K)$. But the same family also has uniformly bounded second
derivatives, so we can extract a further subsequence converging in
$C^1(K)$, and so on. A diagonal argument produces a subsequence converging
in every $C^k(K)$ norm, hence converging in $\mathcal{D}_K$. Since
$\mathcal{D}(\Omega)$ is an inductive limit of the Montel spaces
$\mathcal{D}_K$, it is itself Montel.

**Consequence for $\mathcal{D}'(\Omega)$.** On
$\mathcal{D}'(\Omega)$, there are two natural topologies:

- The **weak-$*$ topology** $\sigma(\mathcal{D}', \mathcal{D})$: pointwise
  convergence on test functions.
- The **strong dual topology** $\beta(\mathcal{D}', \mathcal{D})$: uniform
  convergence on bounded subsets of $\mathcal{D}(\Omega)$.

In a Banach space, these are genuinely different. The Montel property
collapses the gap in four steps:

1. **Pointwise boundedness.** A weak-$*$ convergent sequence $T_n \to T$
   is pointwise bounded: $\sup_n |\langle T_n, \varphi \rangle| < \infty$
   for each $\varphi$.

2. **Equicontinuity (Banach-Steinhaus on Fréchet spaces).** The key step.
   Fix a compact $K \subset \Omega$. The restrictions
   $T_n|_{\mathcal{D}_K}$ are a pointwise bounded family of continuous
   linear functionals on $\mathcal{D}_K$. This is where the Fréchet
   structure of $\mathcal{D}_K$ is essential: because $\mathcal{D}_K$ is a
   complete metrizable space ({prf:ref}`def-D-K`), the Baire
   category theorem applies, and Banach-Steinhaus gives equicontinuity --
   there exist $C_K > 0$ and $k_K \geq 0$ such that
   $|T_n(\varphi)| \leq C_K \|\varphi\|_{K,k_K}$ for *all* $n$ and all
   $\varphi \in \mathcal{D}_K$, simultaneously. (On $\mathcal{D}(\Omega)$
   itself, which is not metrizable, Banach-Steinhaus does not apply
   directly; this is why we must descend to the Fréchet pieces
   $\mathcal{D}_K$ first.)

3. **Uniform convergence on precompact sets.** Equicontinuity +
   pointwise convergence $\Rightarrow$ uniform convergence on every
   precompact subset of $\mathcal{D}(\Omega)$. This is the
   Arzelà-Ascoli principle for functionals: an equicontinuous family that
   converges pointwise converges uniformly on any set where the arguments
   are "close together" (precompact sets are exactly such sets).

4. **Montel: bounded = precompact.** In a Banach space, bounded sets are
   generally *not* precompact (the unit ball is never compact in infinite
   dimensions). The Montel property changes this: every bounded set in
   $\mathcal{D}(\Omega)$ *is* precompact. So uniform convergence on
   precompact sets = uniform convergence on bounded sets = strong
   convergence.

Without Montel, step 4 fails. This is exactly what goes wrong in Banach
spaces, where weak-$*$ and strong convergence are genuinely different.
The chain of reasoning is:

$$\text{weak-$*$ conv.}
\xrightarrow{1} \text{ptwise bounded}
\xrightarrow{2,\text{ Fréchet}} \text{equicontinuous}
\xrightarrow{3} \text{unif. on precompact}
\xrightarrow{4,\text{ Montel}} \text{strong conv.}$$

Therefore **on $\mathcal{D}'(\Omega)$, the weak-$*$ and strong topologies
have the same convergent sequences.** This is why many references simply
say "the topology on $\mathcal{D}'$" without specifying which.
```

### The double dual and non-reflexivity

In the duality chapter, the canonical embedding
$J : X \to X^{**}$, $J(x)(f) = f(x)$, embeds a Banach space into its
double dual. A space is **reflexive** if $J$ is surjective. What happens
for test functions and distributions?

The canonical embedding $J : \mathcal{D}(\Omega) \to
\mathcal{D}'(\Omega)^*$ sends each test function $\varphi$ to the
evaluation functional $J(\varphi)(T) = \langle T, \varphi \rangle$. This
embedding is:

- **Injective**: if $J(\varphi_1) = J(\varphi_2)$, then
  $\langle T, \varphi_1 \rangle = \langle T, \varphi_2 \rangle$ for all
  distributions $T$. By {prf:ref}`prop-separation`, this forces
  $\varphi_1 = \varphi_2$.
- **Not surjective**: there exist continuous linear functionals on
  $\mathcal{D}'(\Omega)$ that do not come from any test function.

```{prf:proposition} $\mathcal{D}(\Omega)$ is not reflexive
:label: prop-not-reflexive

The canonical embedding $J : \mathcal{D}(\Omega) \to
\mathcal{D}'(\Omega)^*$ is not surjective.
```

```{prf:proof}
:class: dropdown

We construct an element of the double dual that is not in the image of $J$.

Let $\{\chi_n\}$ be a sequence of cutoff functions:
$\chi_n \in \mathcal{D}(\Omega)$ with $0 \leq \chi_n \leq 1$,
$\chi_n(x) = 1$ for $x \in K_n$, where $K_1 \subset K_2 \subset \cdots$
is an exhaustion of $\Omega$ by compact sets. Such cutoffs exist by
Urysohn's lemma (or by explicit mollification of characteristic functions).

For any distribution $T \in \mathcal{D}'(\Omega)$ and any test function
$\varphi$, the sequence $\langle T, \chi_n \varphi \rangle \to
\langle T, \varphi \rangle$ since $\chi_n \varphi \to \varphi$ in
$\mathcal{D}(\Omega)$.

Now define $\Lambda : \mathcal{D}'(\Omega) \to \mathbb{R}$ by
$\Lambda(T) = \langle T, \mathbf{1} \rangle$, where the pairing is
understood as $\lim_n \langle T, \chi_n \rangle$ whenever this limit
exists. For every $T \in \mathcal{D}'(\Omega)$, the sequence
$\langle T, \chi_n \rangle$ is eventually constant for distributions
with compact support, and converges for tempered distributions.

On the subspace of compactly supported distributions $\mathcal{E}'(\Omega)$,
$\Lambda$ is a well-defined continuous linear functional. But $\Lambda$
cannot equal $J(\varphi)$ for any $\varphi \in \mathcal{D}(\Omega)$:
that would require $\langle T, \varphi \rangle = \langle T, \mathbf{1}
\rangle$ for all compactly supported $T$, hence $\varphi = \mathbf{1}$.
But $\mathbf{1} \notin \mathcal{D}(\Omega)$, since the constant function $1$
does not have compact support.
```

```{prf:remark}
:label: remark-non-reflexivity-meaning
:class: dropdown

Non-reflexivity means that the bidual $\mathcal{D}'(\Omega)^*$ is strictly
larger than $\mathcal{D}(\Omega)$: there are continuous linear functionals
on the space of distributions that cannot be represented by pairing with
any test function. The constant function $\mathbf{1}$ is the simplest
example: it "pairs" with every compactly supported distribution, but it
is not itself a test function.

Note that this is *not* a statement about weak-$*$ versus strong
convergence; we showed above ({prf:ref}`remark-montel`) that the Montel
property makes those agree on $\mathcal{D}'$. Rather, non-reflexivity is
about the *size* of the dual: the space of test functions is too small
to exhaust all continuous functionals on $\mathcal{D}'$.

Note the role of **Urysohn's lemma** (or equivalently, partitions of
unity): it guarantees the existence of the cutoff functions $\chi_n$ that
approximate $\mathbf{1}$ pointwise. The argument shows that the
"function" $\mathbf{1}$ lives in the bidual but not in $\mathcal{D}$. It
is a phantom test function that distributions can see but test functions
cannot reach.
```

