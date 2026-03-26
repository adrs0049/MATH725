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


### Convergence of measures as weak\* convergence

Measures fit naturally into this picture. By the
{prf:ref}`Riesz-Markov-Kakutani theorem <riesz-markov>`, $C(K)^* \cong
\mathcal{M}(K)$, the space of finite signed Radon measures on a compact
Hausdorff space $K$. Each measure $\mu$ acts as a functional on $C(K)$ via
$\mu(g) = \int_K g\,d\mu$.

```{prf:definition} Total variation norm
:label: tv-norm-def

For a signed measure $\mu = \mu^+ - \mu^-$ (Jordan decomposition), the **total variation norm** is

$$\|\mu\|_{TV} = |\mu|(K) = \mu^+(K) + \mu^-(K).$$

The space $\mathcal{M}(K)$ equipped with $\|\cdot\|_{TV}$ is a Banach space.
```

The total variation norm is the natural "strong" notion of distance between
measures: $\|\mu_n - \mu\|_{TV} \to 0$ means the measures agree on all
measurable sets asymptotically. This is a very demanding requirement.

```{prf:definition} Weak convergence of measures
:label: weak-measures-def

Let $K$ be a compact Hausdorff space and let $(\mu_n)_{n \geq 1}$ be a sequence
in $\mathcal{M}(K)$. We say $\mu_n \rightharpoonup \mu$ **weakly** if

$$\phi(\mu_n) \to \phi(\mu) \quad \text{for every } \phi \in \mathcal{M}(K)^* = C(K)^{**}.$$
```

This is the weak topology on $\mathcal{M}(K)$, which requires testing against
the bidual $C(K)^{**}$. Just as in the general setting, this bidual can be much
larger than $C(K)$ and is difficult to describe explicitly.

```{prf:definition} Weak* convergence of measures
:label: weak-star-measures-def

Let $K$ be a compact Hausdorff space and let $(\mu_n)_{n \geq 1}$ be a sequence in $\mathcal{M}(K) = C(K)^*$. We say $\mu_n \xrightarrow{w^*} \mu$ if

$$\int_K g\,d\mu_n \to \int_K g\,d\mu \quad \text{for every } g \in C(K).$$
```

Weak\* convergence is much more forgiving: it tests only against elements of
$C(K)$, not the full bidual $C(K)^{**}$. This echoes exactly the choice we made
in the general setting.

### Convergence in distribution

If $\mu_n$ and $\mu$ are **probability measures** on $K$ (i.e., $\mu_n \geq 0$,
$\mu_n(K) = 1$), then weak\* convergence in $\mathcal{M}(K) = C(K)^*$ becomes

$$\mathbb{E}_{\mu_n}[g] \to \mathbb{E}_\mu[g] \quad \text{for every continuous } g \in C(K).$$

This is **convergence in distribution** (also called weak convergence of
probability measures in the probability literature). It is the convergence in
the central limit theorem: the *distributions* $\mu_n$ of
$\frac{1}{\sqrt{n}}\sum_{i=1}^n X_i$ converge to the Gaussian measure $\mu$,
meaning the expected value of every continuous test function converges.

```{prf:example} Converging Dirac masses
:label: dirac-weak-star

The sequence $\delta_{1/n}$ converges weak\* to $\delta_0$ in $C([0,1])^*$. Each $\delta_p$ evaluates a function at the point $p$: $\delta_p(g) = g(p)$. As $p = 1/n$ moves toward $0$, continuity gives $g(1/n) \to g(0)$ for every $g \in C([0,1])$.

In total variation, however, $\|\delta_{1/n} - \delta_0\|_{TV} = 2$ for all $n$, since they assign mass to disjoint points. The measures converge in "statistics" (every continuous observable stabilizes) but remain far apart as objects in $\mathcal{M}([0,1])$.
```


### The three convergences for probability measures

| Convergence | Space / pairing | What converges |
|---|---|---|
| **In distribution** (= weak\* in $C(K)^*$) | Measures $\mu_n \in \mathcal{M}(K) = C(K)^*$ | $\int g\,d\mu_n \to \int g\,d\mu$ for all $g \in C(K)$ |
| **In expectation** (= weak in $L^1$) | Random variables $X_n \in L^1(\Omega)$ | $\mathbb{E}[X_n h] \to \mathbb{E}[Xh]$ for all $h \in L^\infty(\Omega)$ |
| **In total variation** (= strong in $\mathcal{M}(K)$) | Measures $\mu_n \in \mathcal{M}(K)$ | $\|\mu_n - \mu\|_{TV} \to 0$ |

Convergence in distribution lives in $C(K)^*$ and only tests against continuous
functions. Convergence in expectation lives in $L^1(\Omega)$ and tests against
all bounded measurable functions (it requires the random variables to be defined
on a common probability space). Total variation convergence is the norm topology
on $\mathcal{M}(K)$.


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
