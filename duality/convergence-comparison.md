---
kernelspec:
  name: python3
  display_name: Python 3
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/convergence-comparison.pdf
    id: duality-convergence-comparison-pdf
downloads:
  - id: duality-convergence-comparison-pdf
    title: Download PDF
---

# Applications of Weak and Weak\* Convergence

:::{tip} Big Idea
The three notions of convergence (strong, weak, weak\*) form a chain of
implications. In probability, they correspond to convergence in $L^1$ norm,
convergence in expectation, and convergence in distribution. The hierarchy of
topologies explains when they coincide (reflexive spaces) and when they diverge.
The **direct method** of the calculus of variations combines Banach-Alaoglu with
weak lower semicontinuity to prove existence of minimizers.
:::

## Convergence in probability: all three in action

The three convergences appear naturally in probability, where they correspond to
familiar notions.

### Convergence in expectation as weak convergence

A random variable $X$ on a probability space $(\Omega, \mathcal{F},
\mathbb{P})$ is an element of $L^1(\Omega, \mathbb{P})$ precisely when it has
**finite expectation**: $\mathbb{E}[|X|] = \int_\Omega |X|\,d\mathbb{P} <
\infty$. The $L^1$ norm *is* the expected absolute value: $\|X\|_{L^1} =
\mathbb{E}[|X|]$.

```{prf:example} Convergence in expectation in $L^1$
:label: convergence-in-expectation

Let $(\Omega, \mathcal{F}, \mathbb{P})$ be a probability space. The Banach space $L^1(\Omega, \mathbb{P})$ has dual $(L^1)^* = L^\infty(\Omega, \mathbb{P})$. Each bounded measurable function $h \in L^\infty$ defines a continuous linear functional on $L^1$ via

$$\varphi_h(X) = \int_\Omega X(\omega)\,h(\omega)\,d\mathbb{P}(\omega) = \mathbb{E}[Xh].$$

Think of $h$ as a **weight function** that selects which parts of $X$ to measure. Typical choices:

- $h = \mathbf{1}_A$ (indicator of a measurable set): $\varphi_h(X) = \int_A X\,d\mathbb{P}$, the integral of $X$ over $A$.
- $h = \text{sgn}(X)$: $\varphi_h(X) = \mathbb{E}[|X|] = \|X\|_{L^1}$, recovering the norm.
- $h = e^{i\xi \cdot (\cdot)}$ (a character, if $\Omega \subseteq \mathbb{R}^d$): $\varphi_h(X) = \widehat{X}(\xi)$, a Fourier coefficient.

A sequence of random variables $X_n \in L^1$ converges **weakly** ($X_n \rightharpoonup X$) if and only if

$$\mathbb{E}[X_n h] \to \mathbb{E}[Xh] \quad \text{for every } h \in L^\infty.$$

In the foliation picture: each weight $h$ defines a foliation of $L^1$, and weak convergence means the "weighted expectation" $\mathbb{E}[X_n h]$ stabilizes for every choice of weight. In particular, taking $h = \mathbf{1}_A$ for every measurable $A$ requires $\int_A X_n\,d\mathbb{P} \to \int_A X\,d\mathbb{P}$: the integrals of $X_n$ agree with those of $X$ over every measurable set.
```

Strong convergence in $L^1$ is $\mathbb{E}[|X_n - X|] \to 0$, which implies weak
convergence but not vice versa. A sequence can have all its weighted
expectations converge without the random variables getting close in the $L^1$
norm.


### Measures and weak\* convergence

The richest example of weak\* convergence in practice is the convergence of
measures. By the Riesz–Markov–Kakutani theorem, $C(K)^* \cong
\mathcal{M}(K)$ (the space of finite signed Radon measures), and weak\*
convergence of measures means $\int g \, d\mu_n \to \int g \, d\mu$ for
every continuous $g$. For probability measures, this is **convergence in
distribution** — the convergence in the central limit theorem.

We develop this fully — including the total variation norm, Wasserstein
distances, tightness, Prokhorov's theorem, and optimal transport — in the
distributions chapter on measure norms. There, the duality framework from
this chapter combines with the distributional framework to give a complete
picture of what different norms on measures "see."


## The direct method: a first look

The combination of Banach-Alaoglu and weak lower semicontinuity is the engine
behind existence proofs in PDE and the calculus of variations. We give a brief
preview here; we will develop this in detail in later sections.

```{prf:definition} Weak lower semicontinuity
:label: weak-lsc-def

A functional $\mathcal{F} \colon X \to \mathbb{R} \cup \{+\infty\}$ is **weakly
lower semicontinuous** if whenever $x_n \rightharpoonup x$ weakly in $X$,

$$\mathcal{F}(x) \leq \liminf_{n \to \infty} \mathcal{F}(x_n).$$
```

The norm itself is the prototypical example: if $x_n \rightharpoonup x$, then
$\|x\| \leq \liminf \|x_n\|$ (this follows from $|f(x)| = \lim |f(x_n)| \leq
\|f\| \liminf \|x_n\|$ for any norming functional $f$). Many energy functionals
in applications inherit this property from convexity.

The **direct method** proceeds in three steps:

1. **Boundedness.** Show that a minimizing sequence $(u_n)$ for $\mathcal{F}$
   is bounded: $\|u_n\| \leq C$.
2. **Compactness.** Extract a weakly convergent subsequence $u_{n_k}
   \rightharpoonup u$. In a reflexive space this is
   {prf:ref}`reflexive-weak-compactness`; in a dual space $X = Y^*$, use
   Banach-Alaoglu ({prf:ref}`banach-alaoglu`) for weak\* compactness instead.
3. **Lower semicontinuity.** Conclude that

$$\mathcal{F}(u) \leq \liminf_{k \to \infty} \mathcal{F}(u_{n_k}) = \inf \mathcal{F},$$

so $u$ is a minimizer.

Step 1 is problem-specific, typically a coercivity estimate. Step 2 is pure
functional analysis, exactly what Banach-Alaoglu and Eberlein-Šmulian provide.
Step 3 requires that $\mathcal{F}$ behaves well under weak limits, which is
where convexity or compensated compactness arguments enter. We will return to
this in detail when we study Sobolev spaces and variational problems.

### The direct method in a reflexive space

```{prf:example} Minimizing the Dirichlet energy
:label: direct-method-dirichlet

Let $\Omega \subset \mathbb{R}^d$ be a bounded open set with smooth boundary,
and fix a boundary datum $g \in H^{1/2}(\partial\Omega)$. Consider the
**Dirichlet energy**

$$\mathcal{E}(u) = \frac{1}{2}\int_\Omega |\nabla u|^2 \, dx$$

over the admissible set $\mathcal{A} = \{u \in H^1(\Omega) : u|_{\partial\Omega} = g\}$.
We claim that $\mathcal{E}$ attains its minimum on $\mathcal{A}$.

**Step 1 (Boundedness).** Let $(u_n)$ be a minimizing sequence:
$\mathcal{E}(u_n) \to \inf_{\mathcal{A}} \mathcal{E}$. Since $\mathcal{E}(u_n)$
is bounded, so is $\|\nabla u_n\|_{L^2}$. The Poincaré inequality (applied to
$u_n - \tilde{g}$ for any fixed extension $\tilde{g} \in H^1(\Omega)$ of $g$)
gives $\|u_n\|_{H^1} \leq C$.

**Step 2 (Compactness).** The Sobolev space $H^1(\Omega) = W^{1,2}(\Omega)$ is
a Hilbert space, hence reflexive. By {prf:ref}`weak-compactness-reflexive`,
the bounded sequence $(u_n)$ has a weakly convergent subsequence
$u_{n_k} \rightharpoonup u$ in $H^1(\Omega)$. The trace operator is
continuous in the weak topology, so $u|_{\partial\Omega} = g$ and $u \in \mathcal{A}$.

**Step 3 (Lower semicontinuity).** The functional $u \mapsto \int_\Omega
|\nabla u|^2 \, dx$ is convex and continuous in the norm topology, so by
Mazur's theorem ({prf:ref}`mazur-theorem`) its sublevel sets are weakly
closed. Equivalently, $\mathcal{E}$ is weakly lower semicontinuous:

$$\mathcal{E}(u) \leq \liminf_{k \to \infty} \mathcal{E}(u_{n_k}) = \inf_{\mathcal{A}} \mathcal{E}.$$

Therefore $u$ is a minimizer. The minimizer is unique by strict convexity of
$\mathcal{E}$, and satisfies the Euler-Lagrange equation $-\Delta u = 0$ in
$\Omega$ (Laplace's equation).
```

The entire argument rests on two pillars: reflexivity of $H^1$ gives weak
compactness, and convexity of $\mathcal{E}$ gives weak lower semicontinuity.
Remove either and the argument collapses.

```{prf:remark} Why convexity gives weak lower semicontinuity
:label: remark-why-lsc

Step 3 is the subtlest part of the direct method. Why can't the energy
*increase* when we pass to a weak limit? There are three ways to see this.

**Direct proof for the Dirichlet energy.** Since $u_{n_k} \rightharpoonup
u$ in $H^1$, we have $\nabla u_{n_k} \rightharpoonup \nabla u$ in $L^2$.
Weak convergence means $\langle \nabla u_{n_k}, w \rangle \to \langle
\nabla u, w \rangle$ for every $w \in L^2$. Taking $w = \nabla u$:

$$\|\nabla u\|_{L^2}^2 = \langle \nabla u, \nabla u \rangle = \lim_k \langle \nabla u_{n_k}, \nabla u \rangle \leq \liminf_k \|\nabla u_{n_k}\|_{L^2} \cdot \|\nabla u\|_{L^2}$$

by Cauchy–Schwarz. Dividing by $\|\nabla u\|_{L^2}$ gives $\|\nabla
u\|_{L^2} \leq \liminf_k \|\nabla u_{n_k}\|_{L^2}$, hence
$\mathcal{E}(u) \leq \liminf_k \mathcal{E}(u_{n_k})$. The same argument
shows that **every norm is weakly lower semicontinuous**: the norm can
only drop under weak limits, never increase.

**Via Mazur's theorem.** More generally, let $\mathcal{F}$ be any convex
and norm-continuous functional. Its sublevel sets $\{u : \mathcal{F}(u)
\leq c\}$ are convex (by convexity of $\mathcal{F}$) and norm-closed (by
continuity). By Mazur's theorem ({prf:ref}`mazur-theorem`), convex
norm-closed sets are weakly closed. So the sublevel sets are weakly closed,
which is equivalent to $\mathcal{F}$ being weakly lower semicontinuous.

**The intuition.** By Mazur's theorem, there exist convex combinations
$v_k = \sum_j \lambda_j^{(k)} u_{n_j}$ converging *strongly* to $u$.
For a convex functional, Jensen's inequality gives

$$\mathcal{F}(v_k) = \mathcal{F}\!\left(\sum_j \lambda_j^{(k)} u_{n_j}\right) \leq \sum_j \lambda_j^{(k)} \mathcal{F}(u_{n_j}).$$

The right-hand side is at most $\max_j \mathcal{F}(u_{n_j})$, which is
eventually close to $\liminf \mathcal{F}(u_{n_k})$. By norm continuity,
$\mathcal{F}(v_k) \to \mathcal{F}(u)$, giving the inequality. In short:
weak limits are limits of averages, and convex functionals can't be fooled
by averaging.
```

### What goes wrong without reflexivity

```{prf:example} Failure of the direct method in $L^1$
:label: direct-method-L1-failure

Consider the functional

$$\mathcal{F}(u) = \left| \int_0^1 u(x) \, dx - 1 \right|$$

over the constraint set $\mathcal{C} = \{u \in L^1([0,1]) : u \geq 0, \
\|u\|_{L^1} = 1\}$. The infimum is $\inf_{\mathcal{C}} \mathcal{F} = 0$,
attained by the constant function $u = 1$.

Now replace the objective with something that rewards concentration. Define

$$\mathcal{G}(u) = -\int_0^1 u(x)^2 \, dx$$

over the same constraint set $\mathcal{C}$. A minimizing sequence is given
by the **approximations to the identity**:

$$u_n(x) = n \, \mathbf{1}_{[0, 1/n]}(x).$$

Each $u_n \in \mathcal{C}$ with $\|u_n\|_{L^1} = 1$ and $\mathcal{G}(u_n) =
-n \to -\infty$, so $\inf_{\mathcal{C}} \mathcal{G} = -\infty$.

But more instructive is what happens to the sequence itself. As measures,
$u_n \, dx \rightharpoonup^* \delta_0$ in $\mathcal{M}([0,1]) = C([0,1])^*$:
for any continuous test function $\varphi$,

$$\int_0^1 \varphi(x) \, u_n(x) \, dx = n \int_0^{1/n} \varphi(x) \, dx \to \varphi(0).$$

The weak-$*$ limit $\delta_0$ is a perfectly good Radon measure, but it does
not belong to $L^1$. The mass has **concentrated** at a single point. This
is the failure mode: $L^1$ is not reflexive, so bounded sequences need not
have weakly convergent subsequences in $L^1$. The sequence escapes to the
larger space of measures, and the direct method cannot recover a minimizer
in the original space.
```

The contrast between {prf:ref}`direct-method-dirichlet` and
{prf:ref}`direct-method-L1-failure` illustrates why reflexivity is not a
technical convenience but a structural requirement. In reflexive spaces, bounded
sets are weakly compact and the direct method closes. In non-reflexive spaces
like $L^1$, minimizing sequences can concentrate or oscillate their way out of
the space, and one must either enlarge the space (to measures) or impose
additional compactness conditions (such as equi-integrability via the
Dunford-Pettis theorem).
