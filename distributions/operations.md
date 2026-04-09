---
kernelspec:
  name: python3
  display_name: Python 3
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/operations.pdf
    id: distributions-operations-pdf
downloads:
  - id: distributions-operations-pdf
    title: Download PDF
---

# The Calculus of Distributions

:::{tip} Big Idea
Every operation on distributions is defined by **duality**: to apply an
operation to a distribution $T$, transfer the adjoint operation to the test
function. Differentiation becomes the integration-by-parts formula, and the
payoff is immediate: every distribution is infinitely differentiable.
:::

The key idea throughout this section is the same: if an operation $A$ on
smooth functions satisfies $\langle Af, \varphi \rangle = \langle f,
A^\dagger \varphi \rangle$ for some adjoint $A^\dagger$ that maps test
functions to test functions, then we *define* $\langle AT, \varphi \rangle
= \langle T, A^\dagger \varphi \rangle$ for any distribution $T$.

**A note on notation.** We have a functional
$T : \mathcal{D}(\Omega) \to \mathbb{R}$, and we want to define a new
functional $AT$. The definition always acts on the test function: $AT$ is
the composition $T \circ A^\dagger$, and $T$ itself is unchanged.
Concretely:

- $D^\alpha T = (-1)^{|\alpha|}\, T \circ D^\alpha$, i.e.
  $\varphi \mapsto (-1)^{|\alpha|} T(D^\alpha \varphi)$,
- $fT = T \circ M_f$, i.e. $\varphi \mapsto T(f\varphi)$, where $M_f$
  is the multiplication operator,
- $\tau_h T = T \circ \tau_{-h}$, i.e.
  $\varphi \mapsto T(\tau_{-h}\varphi)$.

In each case the notation ($D^\alpha T$, $fT$, $\tau_h T$) suggests we are
acting on $T$, but the operation is transferred to $\varphi$ via the
adjoint. This is the adjoint construction from the duality chapter
({prf:ref}`banach-adjoint-def`) applied concretely: if
$A : \mathcal{D}(\Omega) \to \mathcal{D}(\Omega)$ is a continuous linear
map, its adjoint $A^* : \mathcal{D}'(\Omega) \to \mathcal{D}'(\Omega)$
acts by $A^* T = T \circ A$. Differentiation, multiplication, and
translation on distributions are all instances of this. The notation is
justified by consistency: when $T = T_f$ for a classical function $f$, the
distribution $AT$ agrees with the distribution $T_{Af}$ defined by applying
$A$ to $f$ directly.


## Multiplication by Smooth Functions

Given $f \in C^\infty(\Omega)$ and $T \in \mathcal{D}'(\Omega)$, we want
to define a new distribution that deserves the name "$fT$."

```{prf:definition} Multiplication by a smooth function
:label: def-multiplication

Let $f \in C^\infty(\Omega)$ and $T \in \mathcal{D}'(\Omega)$. Define
$U : \mathcal{D}(\Omega) \to \mathbb{R}$ by

$$U(\varphi) = T(f\varphi).$$

We write $fT := U$ and call it the **product** of $f$ and $T$.
```

Note that $U$ is well-defined as a map: $f\varphi \in \mathcal{D}(\Omega)$
whenever $\varphi \in \mathcal{D}(\Omega)$, because the product of a smooth
function and a compactly supported smooth function is again compactly
supported and smooth. So $T(f\varphi)$ makes sense.

```{prf:proposition} Multiplication produces a distribution
:label: prop-multiplication-dist

$fT \in \mathcal{D}'(\Omega)$.
```

```{prf:proof}
:class: dropdown

**Linearity.**

$$U(a\varphi + b\psi) = T(f(a\varphi + b\psi)) = T(af\varphi + bf\psi) = a\,T(f\varphi) + b\,T(f\psi) = a\,U(\varphi) + b\,U(\psi).$$

**Continuity.** Suppose $\varphi_n \to \varphi$ in $\mathcal{D}(\Omega)$
(supports in a fixed compact $K$, all derivatives converge uniformly).
Then $f\varphi_n \to f\varphi$ in $\mathcal{D}(\Omega)$: the supports
remain in $K$, and the Leibniz rule gives

$$D^\alpha(f\varphi_n) = \sum_{\beta \leq \alpha} \binom{\alpha}{\beta} D^\beta f \cdot D^{\alpha-\beta}\varphi_n \to \sum_{\beta \leq \alpha} \binom{\alpha}{\beta} D^\beta f \cdot D^{\alpha-\beta}\varphi = D^\alpha(f\varphi)$$

uniformly on $K$, since $f$ and all its derivatives are bounded on $K$.
Since $T$ is continuous,

$$U(\varphi_n) = T(f\varphi_n) \to T(f\varphi) = U(\varphi).$$
```

```{prf:remark}
:label: remark-multiplication-consistency
:class: dropdown

**Consistency with functions.** When $T = T_g$ for $g \in
L^1_{\mathrm{loc}}(\Omega)$, the distribution $fT_g$ agrees with $T_{fg}$:

$$(fT_g)(\varphi) = T_g(f\varphi) = \int_\Omega g(x)\,f(x)\,\varphi(x)\,dx = T_{fg}(\varphi).$$

So the distributional product extends pointwise multiplication of functions.
```

```{prf:example} Multiplying the Dirac delta
:label: ex-multiply-delta
:class: dropdown

For $f \in C^\infty(\Omega)$:
$(f\delta)(\varphi) = \delta(f\varphi) = f(0)\varphi(0)
= f(0)\,\delta(\varphi)$.
So $f\delta = f(0)\delta$: the delta "evaluates" the smooth factor at its
support.

More generally, $f\delta_{x_0} = f(x_0)\delta_{x_0}$.
```

```{prf:remark}
:label: remark-no-multiply-distributions
:class: dropdown

We cannot multiply two arbitrary distributions. The construction above
requires $f$ to be smooth (or at least sufficiently regular) so that
$\varphi \mapsto f\varphi$ maps $\mathcal{D}(\Omega)$ to itself. The
difficulty of multiplying distributions is a fundamental limitation: it is
related to the problem of renormalization in quantum field theory and was
one of the motivations for Colombeau's theory of generalized functions.
```


## Differentiation of Distributions

With the duality principle now familiar from translation and multiplication,
we come to the main payoff: differentiation.

### The definition

The definition is motivated by integration by parts. Suppose $f$ is smooth.
Then for every $\varphi \in \mathcal{D}(\Omega)$,

$$
\int_\Omega f'(x)\,\varphi(x)\,dx = -\int_\Omega f(x)\,\varphi'(x)\,dx
$$

since the boundary terms vanish (test functions have compact support in
$\Omega$). In the language of distributions:
$T_{f'}(\varphi) = -T_f(\varphi')$. The right-hand side makes sense for
*any* distribution $T$, not just those coming from smooth functions: given
$T \in \mathcal{D}'(\Omega)$, the map $\varphi \mapsto -T(\varphi')$ is
perfectly well-defined. This suggests a definition.

```{prf:definition} Distributional derivative
:label: def-distributional-derivative

Let $T \in \mathcal{D}'(\Omega)$ and $\alpha$ a multi-index. Define
$U : \mathcal{D}(\Omega) \to \mathbb{R}$ by

$$U(\varphi) = (-1)^{|\alpha|}\, T(D^\alpha \varphi).$$

We write $D^\alpha T := U$ and call it the **distributional derivative**
of $T$.
```

```{prf:theorem} Every distribution is infinitely differentiable
:label: thm-distributions-smooth

For any $T \in \mathcal{D}'(\Omega)$ and any multi-index $\alpha$,
$D^\alpha T \in \mathcal{D}'(\Omega)$. In particular, every distribution
can be differentiated infinitely many times.
```

```{prf:proof}
:class: dropdown

Set $U = D^\alpha T$, i.e. $U(\varphi) = (-1)^{|\alpha|}\,T(D^\alpha\varphi)$.

**Linearity.**

$$U(a\varphi + b\psi) = (-1)^{|\alpha|}\,T(D^\alpha(a\varphi + b\psi)) = (-1)^{|\alpha|}\,T(a\,D^\alpha\varphi + b\,D^\alpha\psi) = a\,U(\varphi) + b\,U(\psi).$$

**Continuity.** If $\varphi_n \to \varphi$ in $\mathcal{D}(\Omega)$
(supports in a fixed compact $K$, all derivatives converge uniformly),
then $D^\alpha \varphi_n \to D^\alpha \varphi$ in $\mathcal{D}(\Omega)$
(same compact $K$, all derivatives still converge uniformly — differentiating
does not enlarge supports). Since $T$ is continuous,

$$U(\varphi_n) = (-1)^{|\alpha|}\,T(D^\alpha \varphi_n) \to (-1)^{|\alpha|}\,T(D^\alpha \varphi) = U(\varphi).$$

Since $U$ is linear and continuous, $U \in \mathcal{D}'(\Omega)$. As $T$
and $\alpha$ were arbitrary, we can differentiate again: $D^\beta(D^\alpha T)$
is again a distribution, and so on indefinitely.
```

```{prf:remark}
:label: remark-derivative-consistency
:class: dropdown

**Consistency with functions.** When $T = T_f$ for
$f \in C^{|\alpha|}(\Omega)$, integration by parts gives

$$(D^\alpha T_f)(\varphi) = (-1)^{|\alpha|}\,T_f(D^\alpha\varphi) = (-1)^{|\alpha|}\int_\Omega f\,D^\alpha\varphi\,dx = \int_\Omega D^\alpha f\,\varphi\,dx = T_{D^\alpha f}(\varphi).$$

So the distributional derivative extends the classical one.
```

This is the main payoff of the distributional framework: differentiation
is always possible, and it always produces another distribution.

### The differentiation cascade

The power of distributional derivatives is best seen through a chain of
examples in one dimension ($\Omega = \mathbb{R}$).

```{prf:example} Heaviside to Dirac
:label: ex-heaviside-delta
:class: dropdown

The **Heaviside function** $H(x) = \begin{cases} 1 & x > 0 \\ 0 & x < 0
\end{cases}$ is locally integrable and defines a regular distribution. Its
distributional derivative is the Dirac delta:

$$\langle H', \varphi \rangle = -\langle H, \varphi' \rangle = -\int_0^\infty \varphi'(x)\,dx = \varphi(0) = \langle \delta, \varphi \rangle.$$

So $H' = \delta$ in $\mathcal{D}'(\mathbb{R})$.
```

```{prf:example} The $|x|$ cascade
:label: ex-abs-cascade
:class: dropdown

The function $f(x) = |x|$ is continuous but not differentiable at the
origin. Its distributional derivative is

$$\langle f', \varphi \rangle = -\int_{-\infty}^\infty |x|\,\varphi'(x)\,dx = -\int_{-\infty}^0 (-x)\varphi'(x)\,dx - \int_0^\infty x\,\varphi'(x)\,dx.$$

Integrating by parts on each half-line (boundary terms at $\pm\infty$
vanish because $\varphi$ has compact support; at $0$ the contributions from
both sides cancel):

$$= -\int_{-\infty}^0 \varphi(x)\,dx + \int_0^\infty \varphi(x)\,dx = \int_{-\infty}^\infty \operatorname{sgn}(x)\,\varphi(x)\,dx.$$

So $|x|' = \operatorname{sgn}(x)$ as distributions. Differentiating once more:

$$\langle \operatorname{sgn}', \varphi \rangle = -\int_{-\infty}^\infty \operatorname{sgn}(x)\,\varphi'(x)\,dx = \int_{-\infty}^0 \varphi'(x)\,dx - \int_0^\infty \varphi'(x)\,dx = 2\varphi(0) = \langle 2\delta, \varphi \rangle.$$

The full cascade is:

$$|x| \xrightarrow{D} \operatorname{sgn}(x) \xrightarrow{D} 2\delta_0 \xrightarrow{D} 2\delta_0' \xrightarrow{D} \cdots$$

Each step is well-defined as a distributional derivative. The first step
produces a discontinuous function, the second a measure, and the third an
object that is not even a measure, but all are distributions.
```

```{prf:example} Differentiating $\log|x|$
:label: ex-log-derivative
:class: dropdown

The function $\log|x|$ is locally integrable on $\mathbb{R}$ (the
singularity at the origin is integrable). Its distributional derivative is
the principal value distribution:

$$(\log|x|)' = \mathrm{p.v.}\,\frac{1}{x}$$

in $\mathcal{D}'(\mathbb{R})$. This can be verified by direct computation:

$$\langle (\log|x|)', \varphi \rangle = -\int_{-\infty}^\infty \log|x|\,\varphi'(x)\,dx = \lim_{\varepsilon \to 0} \int_{|x|>\varepsilon} \frac{\varphi(x)}{x}\,dx$$

where the last equality follows from integration by parts on
$(-\infty, -\varepsilon)$ and $(\varepsilon, \infty)$ and observing that
the boundary terms $\log\varepsilon\,[\varphi(\varepsilon) -
\varphi(-\varepsilon)] \to 0$ since $\varphi$ is smooth.
```

### Properties of distributional differentiation

```{prf:proposition} Basic properties
:label: prop-differentiation-properties

Let $S, T \in \mathcal{D}'(\Omega)$, $\alpha, \beta$ multi-indices,
$c \in \mathbb{R}$.

1. **Linearity:** $D^\alpha(cS + T) = cD^\alpha S + D^\alpha T$.

2. **Commutativity of mixed partials:**
   $D^\alpha D^\beta T = D^\beta D^\alpha T = D^{\alpha + \beta} T$.

3. **Consistency:** If $f \in C^{|\alpha|}(\Omega)$, the distributional
   derivative $D^\alpha T_f$ agrees with the classical derivative
   $T_{D^\alpha f}$.

4. **Continuity:** If $T_n \to T$ in $\mathcal{D}'(\Omega)$, then
   $D^\alpha T_n \to D^\alpha T$ in $\mathcal{D}'(\Omega)$.
```

```{prf:proof}
:class: dropdown

All four follow directly from the definition $\langle D^\alpha T, \varphi
\rangle = (-1)^{|\alpha|} \langle T, D^\alpha \varphi \rangle$.

1. Linearity of $T$ in the pairing.

2. $\langle D^\alpha D^\beta T, \varphi \rangle = (-1)^{|\alpha|}
   \langle D^\beta T, D^\alpha \varphi \rangle = (-1)^{|\alpha|+|\beta|}
   \langle T, D^{\alpha+\beta}\varphi \rangle$, which is symmetric in
   $\alpha, \beta$ since partial derivatives of smooth functions commute.

3. For $f \in C^{|\alpha|}$, integration by parts gives $(-1)^{|\alpha|}
   \int f\,D^\alpha \varphi = \int (D^\alpha f)\,\varphi$.

4. If $\langle T_n, \psi \rangle \to \langle T, \psi \rangle$ for all
   $\psi \in \mathcal{D}$, then in particular for $\psi = D^\alpha
   \varphi$: $\langle D^\alpha T_n, \varphi \rangle = (-1)^{|\alpha|}
   \langle T_n, D^\alpha \varphi \rangle \to (-1)^{|\alpha|} \langle T,
   D^\alpha \varphi \rangle = \langle D^\alpha T, \varphi \rangle$.
```

Property 4 is remarkable: **you can always interchange limits and
derivatives in the sense of distributions.** In classical analysis, this
requires uniform convergence of derivatives. In the distributional
framework, pointwise convergence of the functionals is enough, because the
derivative is transferred to the (fixed, smooth) test function.

```{prf:proposition} Leibniz rule for distributions
:label: prop-leibniz

For $f \in C^\infty(\Omega)$ and $T \in \mathcal{D}'(\Omega)$:

$$D(fT) = f'T + fT'$$

and more generally, for any multi-index $\alpha$:

$$D^\alpha(fT) = \sum_{\beta \leq \alpha} \binom{\alpha}{\beta} D^\beta f \cdot D^{\alpha - \beta} T.$$
```

```{prf:proof}
:class: dropdown

For the first-order case in one dimension:

$$\langle D(fT), \varphi \rangle = -\langle fT, \varphi' \rangle = -\langle T, f\varphi' \rangle.$$

Now $f\varphi' = (f\varphi)' - f'\varphi$, so

$$= -\langle T, (f\varphi)' \rangle + \langle T, f'\varphi \rangle = \langle T', f\varphi \rangle + \langle f'T, \varphi \rangle = \langle fT', \varphi \rangle + \langle f'T, \varphi \rangle.$$

The general case follows by induction on $|\alpha|$.
```

### Taylor's theorem for distributions

Now that we have both translation and differentiation, we can combine them
into a distributional Taylor expansion. The idea is simple: to expand
$\tau_h T$ in powers of $h$, apply $\tau_h T$ to a test function and use
the classical Taylor expansion of $\varphi(x + h)$ in $h$.

```{prf:theorem} Taylor's theorem for distributions
:label: thm-taylor-distributions

Let $T \in \mathcal{D}'(\mathbb{R}^d)$ and $h \in \mathbb{R}^d$. Then for
every $N \geq 0$,

$$\tau_h T = \sum_{|\alpha| \leq N} \frac{(-h)^\alpha}{\alpha!}\, D^\alpha T + R_N$$

where the remainder $R_N \in \mathcal{D}'(\mathbb{R}^d)$ satisfies

$$R_N(\varphi) = T\!\left( \sum_{|\alpha| = N+1} \frac{h^\alpha}{\alpha!} \int_0^1 (1-t)^N\, (D^\alpha\varphi)(\cdot + th)\, (N+1)\,dt \right)$$

for all $\varphi \in \mathcal{D}(\mathbb{R}^d)$.
```

```{prf:proof}
:class: dropdown

By definition, $(\tau_h T)(\varphi) = T(\tau_{-h}\varphi)
= T(\varphi(\cdot + h))$. Since $\varphi$ is smooth, we apply the
classical Taylor expansion in the variable $h$: for each fixed $x$,

$$\varphi(x + h) = \sum_{|\alpha| \leq N} \frac{h^\alpha}{\alpha!}\, D^\alpha\varphi(x) + \sum_{|\alpha| = N+1} \frac{h^\alpha}{\alpha!} \int_0^1 (1-t)^N\, (D^\alpha\varphi)(x + th)\,(N+1)\,dt.$$

This expansion, and all its $x$-derivatives, converge uniformly on compact
sets (the remainder and its derivatives are controlled by finitely many
derivatives of $\varphi$ on a compact set containing
$\operatorname{supp}(\varphi) + [0,1] \cdot h$). So the expansion holds in
$\mathcal{D}(\mathbb{R}^d)$. Applying $T$:

$$(\tau_h T)(\varphi) = \sum_{|\alpha| \leq N} \frac{h^\alpha}{\alpha!}\, T(D^\alpha\varphi) + T(\text{remainder}).$$

Now $T(D^\alpha\varphi) = (-1)^{|\alpha|}(D^\alpha T)(\varphi)$, so

$$(\tau_h T)(\varphi) = \sum_{|\alpha| \leq N} \frac{(-h)^\alpha}{\alpha!}\, (D^\alpha T)(\varphi) + R_N(\varphi).$$
```

```{prf:example} Taylor expansion of $\delta_h$
:label: ex-taylor-delta
:class: dropdown

Taking $T = \delta$ and $d = 1$: since $\tau_h\delta = \delta_h$
({prf:ref}`ex-translate-delta`), the Taylor formula gives

$$\delta_h = \sum_{n=0}^{N} \frac{(-h)^n}{n!}\, \delta^{(n)} + R_N.$$

Let us verify this directly. Applying both sides to a test function
$\varphi$:

$$\varphi(h) = \sum_{n=0}^{N} \frac{(-h)^n}{n!}\, \delta^{(n)}(\varphi) + R_N(\varphi) = \sum_{n=0}^{N} \frac{(-h)^n}{n!}\,(-1)^n\,\varphi^{(n)}(0) + R_N(\varphi) = \sum_{n=0}^{N} \frac{h^n}{n!}\,\varphi^{(n)}(0) + R_N(\varphi).$$

This is exactly the classical Taylor expansion of $\varphi$ at $0$,
evaluated at $h$. The distributional Taylor theorem for $\delta$ is
nothing but the classical Taylor theorem for the test function, read
through the duality.
```


## Weak Derivatives

Distributional derivatives exist for every distribution, but they may not
be representable by a function. When they are, we get the notion of a
**weak derivative**, which bridges distribution theory and Sobolev spaces.

```{prf:definition} Weak derivative
:label: def-weak-derivative

Let $u \in L^1_{\mathrm{loc}}(\Omega)$. We say $u$ has a **weak
derivative** $D^\alpha u = v$ if there exists $v \in
L^1_{\mathrm{loc}}(\Omega)$ such that

$$\int_\Omega u\,D^\alpha \varphi\,dx = (-1)^{|\alpha|} \int_\Omega v\,\varphi\,dx \qquad \text{for all } \varphi \in \mathcal{D}(\Omega).$$

When it exists, the weak derivative is unique (up to a.e. equivalence).
```

In the language of adjoints: the distributional derivative
$D^\alpha T_u$ is the functional
$\varphi \mapsto (-1)^{|\alpha|} \int u\, D^\alpha\varphi\, dx$. This
always defines an element of $\mathcal{D}'(\Omega)$. The question is
whether this functional can be *represented* by a function $v$ via
$\varphi \mapsto \int v\,\varphi\, dx$. When it can, $v = D^\alpha u$ is the weak derivative of $u$. If moreover
$u \in L^p$ and $D^\alpha u \in L^p$, then $u$ belongs to a **Sobolev
space** $W^{k,p}(\Omega)$: the space of $L^p$ functions whose weak
derivatives up to order $k$ are also in $L^p$. Sobolev spaces are the natural home for
PDE solutions that are not classically differentiable, and their theory
rests entirely on the distinction between distributional and weak
derivatives.

```{prf:example} $|x|$ has a weak derivative
:label: ex-abs-weak
:class: dropdown

By {prf:ref}`ex-abs-cascade`, the distributional derivative of $|x|$ is
$\operatorname{sgn}(x)$. Since $\operatorname{sgn} \in
L^1_{\mathrm{loc}}(\mathbb{R})$, this is a genuine weak derivative:
$|x|' = \operatorname{sgn}(x)$ weakly.

Note that $|x|$ is not classically differentiable at the origin, but the
single point $\{0\}$ has measure zero and does not affect the $L^1_{\mathrm{loc}}$
function $\operatorname{sgn}(x)$.
```

```{prf:example} The Heaviside function has no weak derivative in $L^1_{\mathrm{loc}}$
:label: ex-heaviside-no-weak
:class: dropdown

By {prf:ref}`ex-heaviside-delta`, $H' = \delta$ as distributions. But
$\delta$ is not a regular distribution: there is no $v \in
L^1_{\mathrm{loc}}(\mathbb{R})$ with $\int v\,\varphi\,dx = \varphi(0)$
for all test functions $\varphi$. So $H$ does **not** have a weak
derivative.

This is why $H \in L^p(\Omega)$ for any bounded $\Omega$ but $H \notin
W^{1,p}(\Omega)$ for any $p$: membership in the Sobolev space requires the
weak derivative to exist *as a function in $L^p$*.
```

```{prf:example} Characteristic function of an interval
:label: ex-char-function
:class: dropdown

The function $u = \mathbf{1}_{(a,b)}$ has distributional derivative
$u' = \delta_a - \delta_b$ (a difference of point masses). This is a
measure but not in $L^1_{\mathrm{loc}}$, so $u$ has no weak derivative.
Like the Heaviside function, $u \in L^p$ but $u \notin W^{1,p}$ for any
$p$.
```

```{prf:remark}
:label: remark-weak-vs-classical
:class: dropdown

The weak derivative extends the classical derivative in the following sense:

- If $f$ is classically differentiable (or even just absolutely continuous),
  its weak derivative exists and agrees with the classical derivative a.e.
- Weak differentiability allows corners and kinks (finitely many, or even
  countably many, as long as the derivative remains locally integrable).
- Weak differentiability does **not** allow jumps: a jump discontinuity
  produces a delta function in the derivative, which is not in
  $L^1_{\mathrm{loc}}$.

The dividing line is **absolute continuity**: a function $u$ on an interval
has a weak derivative in $L^1_{\mathrm{loc}}$ if and only if $u$ is
(equivalent to) an absolutely continuous function.
```


## Translation and Reflection

The simplest operations on distributions illustrate the duality principle
with no calculus required.

Recall that for functions on $\mathbb{R}^d$, translation by
$h \in \mathbb{R}^d$ is $(\tau_h \varphi)(x) = \varphi(x - h)$ and
reflection is $\check{\varphi}(x) = \varphi(-x)$. Given a distribution
$T \in \mathcal{D}'(\mathbb{R}^d)$, we want to define the translated
distribution $\tau_h T$ and the reflected distribution $\check{T}$.

```{prf:definition} Translation and reflection of distributions
:label: def-translation-reflection

Let $T \in \mathcal{D}'(\mathbb{R}^d)$.

1. Define $U_h : \mathcal{D}(\mathbb{R}^d) \to \mathbb{R}$ by
   $U_h(\varphi) = T(\tau_{-h}\varphi)$. We write $\tau_h T := U_h$ and
   call it the **translation** of $T$ by $h$.

2. Define $V : \mathcal{D}(\mathbb{R}^d) \to \mathbb{R}$ by
   $V(\varphi) = T(\check{\varphi})$. We write $\check{T} := V$ and call
   it the **reflection** of $T$.
```

```{prf:proposition} Translation and reflection produce distributions
:label: prop-translation-reflection-dist

$\tau_h T$ and $\check{T}$ are distributions, i.e. they belong to
$\mathcal{D}'(\mathbb{R}^d)$.
```

```{prf:proof}
:class: dropdown

We verify the two requirements for $U_h = \tau_h T$; the argument for
$V = \check{T}$ is identical.

**Linearity.**

$$U_h(a\varphi + b\psi) = T(\tau_{-h}(a\varphi + b\psi)) = T(a\,\tau_{-h}\varphi + b\,\tau_{-h}\psi) = a\,T(\tau_{-h}\varphi) + b\,T(\tau_{-h}\psi) = a\,U_h(\varphi) + b\,U_h(\psi).$$

**Continuity.** If $\varphi_n \to \varphi$ in $\mathcal{D}(\mathbb{R}^d)$
(supports in a fixed compact $K$, all derivatives converge uniformly),
then $\tau_{-h}\varphi_n \to \tau_{-h}\varphi$ in
$\mathcal{D}(\mathbb{R}^d)$ (supports in the fixed compact $K + h$, all
derivatives still converge uniformly). Since $T$ is continuous,

$$U_h(\varphi_n) = T(\tau_{-h}\varphi_n) \to T(\tau_{-h}\varphi) = U_h(\varphi).$$
```

```{prf:remark}
:label: remark-translation-consistency
:class: dropdown

**Consistency with functions.** When $T = T_f$ for $f \in
L^1_{\mathrm{loc}}$, the distribution $\tau_h T_f$ agrees with
$T_{\tau_h f}$:

$$(\tau_h T_f)(\varphi) = T_f(\tau_{-h}\varphi) = \int f(x)\,\varphi(x+h)\,dx = \int f(y-h)\,\varphi(y)\,dy = T_{\tau_h f}(\varphi).$$

So the distributional definition extends the classical one.
```

```{prf:example} Translation of the Dirac delta
:label: ex-translate-delta
:class: dropdown

$(\tau_h \delta)(\varphi) = \delta(\tau_{-h}\varphi)
= (\tau_{-h}\varphi)(0) = \varphi(h) = \delta_h(\varphi)$.
So $\tau_h \delta = \delta_h$: translating the delta moves the
point of evaluation.
```


## Convolution

Convolution with a test function is a smoothing operation: it always
produces a smooth function, even when applied to a distribution. The
definition uses translation and reflection from the preceding section.

### Convolution of functions (review)

For $f \in L^1_{\mathrm{loc}}(\mathbb{R}^d)$ and $\psi \in
\mathcal{D}(\mathbb{R}^d)$:

$$(f * \psi)(x) = \int_{\mathbb{R}^d} f(y)\,\psi(x - y)\,dy.$$

The result $f * \psi$ is smooth ($C^\infty$) and satisfies $D^\alpha(f *
\psi) = f * D^\alpha \psi$.

### Convolution of a distribution with a test function

```{prf:definition} Convolution with a test function
:label: def-convolution

Let $T \in \mathcal{D}'(\mathbb{R}^d)$ and $\psi \in
\mathcal{D}(\mathbb{R}^d)$. The **convolution** $T * \psi$ is the function

$$(T * \psi)(x) = \langle T, \tau_x\check{\psi} \rangle = \langle T_y, \psi(x - y) \rangle$$

where $\tau_x$ is translation ({prf:ref}`def-translation-reflection`),
$\check{\psi}$ is reflection, and $T$ acts on the $y$ variable.
```

When $T = T_f$ for a locally integrable function $f$, this recovers the
usual convolution: $(T_f * \psi)(x) = \int f(y)\,\psi(x-y)\,dy = (f *
\psi)(x)$.

```{prf:theorem} Regularization by convolution
:label: thm-regularization

Let $T \in \mathcal{D}'(\mathbb{R}^d)$ and $\psi \in
\mathcal{D}(\mathbb{R}^d)$. Then:

1. $T * \psi \in C^\infty(\mathbb{R}^d)$: the result is always a smooth
   function.

2. $D^\alpha(T * \psi) = (D^\alpha T) * \psi = T * (D^\alpha \psi)$.

3. $\operatorname{supp}(T * \psi) \subseteq \operatorname{supp}(T) +
   \operatorname{supp}(\psi)$ (Minkowski sum).
```

```{prf:proof}
:class: dropdown

**Smoothness.** Fix $x_0 \in \mathbb{R}^d$ and consider the map $x \mapsto
\tau_x\check{\psi}$ from $\mathbb{R}^d$ into $\mathcal{D}(\mathbb{R}^d)$.
This map is smooth: for any direction $e_i$,

$$\lim_{h \to 0} \frac{\tau_{x_0 + he_i}\check{\psi} - \tau_{x_0}\check{\psi}}{h} = \partial_i[\tau_{x_0}\check{\psi}]$$

and the convergence holds in $\mathcal{D}(\mathbb{R}^d)$ (all supports
stay in a fixed compact set, all derivatives converge uniformly).
Applying the continuous linear functional $T$:

$$\partial_i(T * \psi)(x_0) = \lim_{h \to 0} \frac{\langle T, \tau_{x_0 + he_i}\check{\psi}\rangle - \langle T, \tau_{x_0}\check{\psi} \rangle}{h} = \langle T, \partial_i[\tau_{x_0}\check{\psi}] \rangle.$$

Iterating gives smoothness to all orders.

**Interchange of derivative and convolution.** From the proof above,
$D^\alpha(T * \psi)(x) = \langle T, D^\alpha_x \psi(x - \cdot) \rangle =
(T * D^\alpha \psi)(x)$. For the other identity, $\langle D^\alpha T,
\psi(x - \cdot) \rangle = (-1)^{|\alpha|} \langle T, D^\alpha_y \psi(x -
y) \rangle = \langle T, D^\alpha_x \psi(x - \cdot) \rangle$, using the
chain rule $D^\alpha_y \psi(x - y) = (-1)^{|\alpha|} D^\alpha_x \psi(x -
y)$.
```

### Approximation to the identity

```{prf:definition} Mollifier
:label: def-mollifier

A **mollifier** (or approximation to the identity) is a family
$\{\rho_\varepsilon\}_{\varepsilon > 0}$ of test functions satisfying:

1. $\rho_\varepsilon \geq 0$,
2. $\int \rho_\varepsilon = 1$,
3. $\operatorname{supp}(\rho_\varepsilon) \subseteq B(0, \varepsilon)$.

The standard choice is $\rho_\varepsilon(x) =
\varepsilon^{-d}\rho(x/\varepsilon)$ where $\rho$ is a fixed non-negative
test function with $\int \rho = 1$ supported in the unit ball.
```

```{prf:theorem} Mollification approximates distributions
:label: thm-mollification

Let $T \in \mathcal{D}'(\mathbb{R}^d)$ and $\{\rho_\varepsilon\}$ a
mollifier. Then:

1. Each $T * \rho_\varepsilon$ is a smooth function.
2. $T * \rho_\varepsilon \to T$ in $\mathcal{D}'(\mathbb{R}^d)$ as
   $\varepsilon \to 0$.
3. If $T = T_f$ for $f \in L^p(\mathbb{R}^d)$, $1 \leq p < \infty$, then
   $f * \rho_\varepsilon \to f$ in $L^p$.
```

This is one of the most useful results in analysis: every distribution
can be approximated by smooth functions. This is the distributional
analogue of sequential density ({prf:ref}`prop-sequential-density`), made
constructive.

