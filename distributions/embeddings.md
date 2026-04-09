---
kernelspec:
  name: python3
  display_name: Python 3
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/embeddings.pdf
    id: distributions-embeddings-pdf
downloads:
  - id: distributions-embeddings-pdf
    title: Download PDF
---

# Sobolev Embeddings

:::{tip} Big Idea
Controlling derivatives forces better integrability and even continuity.
The Sobolev embedding theorem makes this precise: $s$ derivatives in $L^p$
"buy" integrability up to $L^{p^*}$ (or continuity if $sp > d$). The
exchange rate is governed by an **uncertainty principle**: a function
oscillating at frequency $N$ must spread over width at least $N^{-1/d}$,
and the critical exponent $p^*$ is exactly where this trade-off saturates.
:::


## From Sobolev regularity to integrability

The Sobolev norm controls more than just derivatives; it forces the function
to have better integrability and even continuity, depending on how many
derivatives are controlled. The simplest and most instructive instance is the
Poincaré inequality.

### The Poincaré inequality: controlling variation by the gradient

```{prf:theorem} Poincaré inequality
:label: poincare-inequality

Let $\Omega \subset \mathbb{R}^d$ be a bounded, connected open set with
Lipschitz boundary. There exists a constant $C = C(\Omega)$ such that for
all $u \in H^1(\Omega)$,

$$\|u - \bar{u}\|_{L^2(\Omega)} \leq C \|\nabla u\|_{L^2(\Omega)},$$

where $\bar{u} = \frac{1}{|\Omega|}\int_\Omega u \, dx$ is the mean of $u$.

For $u \in H^1_0(\Omega)$ (zero boundary values), the mean drops out:

$$\|u\|_{L^2(\Omega)} \leq C \|\nabla u\|_{L^2(\Omega)}.$$
```

The interpretation is direct: **if the gradient is small, the function
cannot deviate far from its mean**. A function with small $\|\nabla u\|_{L^2}$
is nearly constant on $\Omega$.

````{prf:proof}
:class: dropdown

We prove the $H^1_0$ version in one dimension: $\Omega = (0, L)$, $u(0) = 0$.

For any $x \in (0, L)$, the fundamental theorem of calculus gives

$$u(x) = \int_0^x u'(t) \, dt.$$

By Cauchy-Schwarz:

$$|u(x)|^2 = \left|\int_0^x u'(t) \, dt\right|^2 \leq x \int_0^x |u'(t)|^2 \, dt \leq L \int_0^L |u'(t)|^2 \, dt = L \|u'\|_{L^2}^2.$$

Integrating over $x \in (0, L)$:

$$\|u\|_{L^2}^2 = \int_0^L |u(x)|^2 \, dx \leq L^2 \|u'\|_{L^2}^2.$$

So $\|u\|_{L^2} \leq L \|u'\|_{L^2}$, with constant $C = L$.
````

The Poincaré inequality connects to everything we have seen:

**The frequency picture.** On the interval $(0, L)$ with zero boundary
conditions, the eigenfunctions of $-\Delta$ are $\sin(n\pi x/L)$ with
eigenvalues $\lambda_n = (n\pi/L)^2$. For $u = \sum_n \hat{u}_n \sin(n\pi x/L)$:

$$\|u\|_{L^2}^2 = \sum_n |\hat{u}_n|^2, \qquad \|\nabla u\|_{L^2}^2 = \sum_n \frac{n^2\pi^2}{L^2} |\hat{u}_n|^2.$$

The Poincaré inequality $\|u\|_{L^2} \leq C \|\nabla u\|_{L^2}$ is equivalent to

$$\sum_n |\hat{u}_n|^2 \leq C^2 \sum_n \frac{n^2\pi^2}{L^2} |\hat{u}_n|^2,$$

which holds with $C = L/\pi$ because every term on the right is at least
$({\pi}/{L})^2$ times the corresponding term on the left. The optimal constant
is $C = L/\pi$, attained by the lowest eigenfunction $\sin(\pi x/L)$: the
function that oscillates as slowly as possible.

**The direct method.** The Poincaré inequality is what made Step 1
(boundedness) work in {prf:ref}`direct-method-dirichlet`: a bound on
$\|\nabla u_n\|_{L^2}$ (from the energy) gives a bound on $\|u_n\|_{L^2}$
(via Poincaré), hence on $\|u_n\|_{H^1}$. Without Poincaré, controlling
the energy would not give a bounded sequence in $H^1$.

**The variance interpretation.** The Poincaré inequality says: the **variance**
of $u$ (how much it deviates from its mean) is controlled by the **total
variation** of $u$ (how much it changes). If $u$ is thought of as a signal,
small gradient means small variation means nearly constant. In probability,
the analog is: the variance of a random variable is bounded by the expected
squared gradient (the Fisher information).

### The general embedding picture

```{prf:theorem} Sobolev embedding theorem
:label: sobolev-embedding-theorem

Let $\Omega \subseteq \mathbb{R}^d$ be open with suitable regularity (e.g.,
Lipschitz boundary or $\Omega = \mathbb{R}^d$).

1. **Subcritical case** ($kp < d$): $W^{k,p}(\Omega) \hookrightarrow
   L^{p^*}(\Omega)$ where $p^* = dp/(d - kp)$ is the **Sobolev conjugate**.
   Controlling $k$ derivatives in $L^p$ gives integrability up to $L^{p^*}$.

2. **Critical case** ($kp = d$): $W^{k,p}(\Omega) \hookrightarrow
   L^q(\Omega)$ for all $q < \infty$ (but not $L^\infty$ in general).
   The function is "almost continuous" but may have logarithmic
   singularities.

3. **Supercritical case** ($kp > d$): $W^{k,p}(\Omega) \hookrightarrow
   C^{m,\alpha}(\overline{\Omega})$ for appropriate $m$ and $\alpha$.
   Controlling enough derivatives in $L^p$ forces continuity (and even
   Holder regularity).
```


## The uncertainty principle

The Sobolev embedding theorem says that controlling $k$ derivatives in $L^p$
forces membership in $L^{p^*}$ with $1/p^* = 1/p - k/d$. Where does this
critical exponent come from? The answer is an **uncertainty principle**: a
function cannot be simultaneously localized in both space and frequency.

### Two regimes of the model function

Return to the model function $f_{A,R,N}(x) = A\,\phi(x/R)\,\sin(Nx)$.
Its derivative is

$$f_{A,R,N}'(x) = \frac{A}{R}\,\phi'(x/R)\,\sin(Nx) + A\,N\,\phi(x/R)\,\cos(Nx).$$

There are two competing terms:
- The **envelope term** $A/R \cdot \phi'(x/R)\sin(Nx)$, from differentiating the bump,
- The **oscillation term** $AN \cdot \phi(x/R)\cos(Nx)$, from differentiating the sine.

Which term dominates depends on the relationship between $R$ and $N$:

**The well-behaved regime: $R \geq 1/N$.** The oscillation term dominates:
$\|f'\|_p \sim AN\,R^{1/p}$. The function completes many oscillations
within its support, and derivatives faithfully measure the frequency. The
Sobolev norm behaves as the heuristic predicts:
$\|f\|_{W^{1,p}} \approx A\,R^{1/p}\,N$.

**The ill-behaved regime: $R < 1/N$.** The envelope term dominates:
$\|f'\|_p \sim A\,R^{1/p - 1}$. The function is so narrow that it does not
complete even one oscillation. The "frequency" $N$ is invisible, and the
derivative is controlled by the compression $1/R$ of the bump.

The following plot illustrates both regimes.

```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(-3, 3, 2000)

def bump(x):
    """Smooth bump function supported on [-1, 1]."""
    result = np.zeros_like(x)
    mask = np.abs(x) < 1
    result[mask] = np.exp(-1 / (1 - x[mask]**2))
    return result / np.max(result)  # normalize peak to 1

fig, axes = plt.subplots(2, 2, figsize=(10, 6))

# Well-behaved regime: R = 1, N = 20 (R >> 1/N)
R1, N1 = 1.0, 20
f1 = bump(x / R1) * np.sin(N1 * x)
f1_env = bump(x / R1)

axes[0, 0].plot(x, f1, 'C0', lw=0.8)
axes[0, 0].plot(x, f1_env, 'C3', lw=1.2, ls='--', label='envelope $\\phi(x/R)$')
axes[0, 0].plot(x, -f1_env, 'C3', lw=1.2, ls='--')
axes[0, 0].set_title(f'Well-behaved: $R={R1}$, $N={N1}$  ($R \\gg 1/N$)', fontsize=10)
axes[0, 0].set_ylabel('$f_{A,R,N}(x)$')
axes[0, 0].legend(fontsize=8)

# Its derivative
dx = x[1] - x[0]
f1_deriv = np.gradient(f1, dx)
axes[1, 0].plot(x, f1_deriv, 'C0', lw=0.8)
axes[1, 0].set_title(f'Derivative: oscillation term $\\sim N$ dominates', fontsize=10)
axes[1, 0].set_ylabel("$f'_{A,R,N}(x)$")
axes[1, 0].set_xlabel('$x$')

# Ill-behaved regime: R = 0.02, N = 20 (R < 1/N = 0.05)
R2, N2 = 0.02, 20
f2 = bump(x / R2) * np.sin(N2 * x)
f2_env = bump(x / R2)

axes[0, 1].plot(x, f2, 'C0', lw=1.2)
axes[0, 1].plot(x, f2_env, 'C3', lw=1.2, ls='--', label='envelope $\\phi(x/R)$')
axes[0, 1].plot(x, -f2_env, 'C3', lw=1.2, ls='--')
axes[0, 1].set_title(f'Ill-behaved: $R={R2}$, $N={N2}$  ($R < 1/N$)', fontsize=10)
axes[0, 1].set_xlim(-0.15, 0.15)

axes[0, 1].legend(fontsize=8)

# Its derivative
f2_deriv = np.gradient(f2, dx)
axes[1, 1].plot(x, f2_deriv, 'C0', lw=1.2)
axes[1, 1].set_title(f'Derivative: envelope term $\\sim 1/R$ dominates', fontsize=10)
axes[1, 1].set_xlabel('$x$')
axes[1, 1].set_xlim(-0.15, 0.15)

for ax in axes.flat:
    ax.axhline(0, color='gray', lw=0.5, zorder=0)
    ax.grid(True, alpha=0.3)

fig.suptitle('The uncertainty principle: well-behaved vs. ill-behaved regimes',
             fontsize=12, fontweight='bold', y=1.01)
plt.tight_layout()
plt.show()
```

The dividing line between these regimes is the **uncertainty principle for
functions**:

$$\boxed{R^d \cdot N \geq 1.}$$

A function oscillating at frequency $N$ must spread over a region of width
at least $R \geq N^{-1/d}$. In one dimension, this says the support must
be at least one wavelength wide. In $d$ dimensions, the *volume* $R^d$
must be at least $1/N$.

```{prf:remark} Classical uncertainty and Sobolev embedding
:label: uncertainty-sobolev
:class: dropdown

The classical Fourier uncertainty principle states: if $f$ is concentrated
in an interval of width $\Delta x$, then its Fourier transform $\hat{f}$
must be spread over a frequency range $\Delta\xi$ with $\Delta x \cdot
\Delta\xi \geq 1$. A function cannot be simultaneously localized in both
space and frequency.

The Sobolev embedding theorem is the *quantitative* form of this
principle. Trading $s$ derivatives of regularity (frequency control) for
integrability (spatial behavior) is precisely the trade-off between
frequency localization and spatial localization. The critical exponent
$1/q = 1/p - s/d$ quantifies the exchange rate: each derivative "buys"
$1/d$ units of integrability, exactly the rate dictated by the uncertainty
constraint $R^d N \geq 1$.
```

### Deriving the critical exponent from the uncertainty principle

Fix $\|f_{A,R,N}\|_{W^{s,p}} = 1$, so $A \approx R^{-1/p} N^{-s}$. The
$L^q$ norm is $\|f\|_{L^q} \approx A\,R^{1/q} = R^{1/q - 1/p}\,N^{-s}$.

We want to find the largest $q$ such that $\|f\|_{L^q}$ remains bounded for
*all* well-behaved functions (all $R, N$ with $R \geq N^{-1/d}$). The
function that makes the $L^q$ norm largest (the one that concentrates the
most energy into the smallest region while respecting the uncertainty
constraint) sits at the boundary $R = N^{-1/d}$. Substituting:

$$\|f\|_{L^q} \approx N^{(1/p - 1/q)/d - s}.$$

This is bounded for all $N \geq 1$ if and only if $(1/p - 1/q)/d \leq s$,
i.e., $1/q \geq 1/p - s/d$. The critical case gives exactly the Sobolev
exponent:

$$\frac{1}{q} = \frac{1}{p} - \frac{s}{d} \qquad \Longleftrightarrow \qquad q = p^* = \frac{dp}{d - sp}.$$

Functions at the uncertainty boundary $R = N^{-1/d}$ are the **extremizers**
of the embedding: they are as concentrated as the uncertainty principle
allows, making the $L^q$ norm as large as possible for a given $W^{s,p}$
norm. The Sobolev embedding theorem says that even these extremal functions
have bounded $L^{p^*}$ norm.


## Compact embeddings: Rellich-Kondrachov

The Sobolev embedding theorem tells us that a bounded set in $W^{k,p}$ is
bounded in $L^{p^*}$. However, **bounded** in an infinite-dimensional space
does not mean **precompact** ({prf:ref}`rem-compact-sets-inf-dim`). The
remarkable fact is that if we ask for slightly less integrability ($q < p^*$
instead of $q = p^*$), the embedding becomes **compact**: bounded sequences
not only stay bounded but have convergent subsequences.

```{prf:theorem} Rellich-Kondrachov compactness
:label: rellich-kondrachov

Let $\Omega \subset \mathbb{R}^d$ be bounded with Lipschitz boundary. Then
for $kp < d$, the embedding

$$W^{k,p}(\Omega) \hookrightarrow L^q(\Omega)$$

is **compact** for $1 \leq q < p^*$ (strict inequality). For $kp > d$, the
embedding $W^{k,p}(\Omega) \hookrightarrow C(\overline{\Omega})$ is compact.
```

````{prf:proof}
:class: dropdown

We prove the key case $H^1(\Omega) \hookrightarrow L^2(\Omega)$ using
Fourier analysis; the general case follows the same logic.

Recall from {prf:ref}`def-compact-precompact` that a set in a complete
metric space is precompact if and only if it is **totally bounded**,
coverable by finitely many $\varepsilon$-balls at every scale. Total
boundedness is **approximate finite-dimensionality**: at resolution
$\varepsilon$, the set is indistinguishable from a finite set.

Let $B = \{u \in H^1(\Omega) : \|u\|_{H^1} \leq 1\}$ and consider $B$
as a subset of $L^2(\Omega)$. Working on a bounded domain (or torus) with
Fourier basis $\{e_k\}$, every $u \in B$ has an expansion
$u = \sum_k \hat{u}_k e_k$ with

$$\sum_k (1 + |k|^2)\,|\hat{u}_k|^2 = \|u\|_{H^1}^2 \leq 1.$$

Split $u$ into low and high frequencies at a cutoff $N$:

$$u = \underbrace{\sum_{|k| \leq N} \hat{u}_k\, e_k}_{u_{\leq N}} + \underbrace{\sum_{|k| > N} \hat{u}_k\, e_k}_{u_{>N}}.$$

**The high-frequency tail is uniformly small.** For every $u \in B$:

$$\|u_{>N}\|_{L^2}^2 = \sum_{|k|>N} |\hat{u}_k|^2 \leq \frac{1}{1 + N^2} \sum_{|k|>N} (1 + |k|^2)\,|\hat{u}_k|^2 \leq \frac{1}{1 + N^2}.$$

This bound is **uniform over all $u \in B$**: it depends only on $N$, not
on the particular function. Given any $\varepsilon > 0$, choose $N$ large
enough that $1/(1+N^2) < \varepsilon^2$.

**The low-frequency part is finite-dimensional.** The projection
$u \mapsto u_{\leq N}$ maps $B$ into the span of the finitely many modes
$\{e_k : |k| \leq N\}$, which is a finite-dimensional subspace of $L^2$.
A bounded set in a finite-dimensional space is precompact
(Bolzano-Weierstrass).

**Combining:** every element of $B$ is within $\varepsilon$ (in $L^2$) of
the precompact set $\{u_{\leq N} : u \in B\}$. A set that can be
approximated to arbitrary accuracy by precompact sets is itself precompact.
So $B$ is precompact in $L^2$, i.e. the embedding is compact.
````

### The two pathologies and the Arzelà-Ascoli analogy

There are exactly two ways a bounded sequence in $L^2$ can fail to be
precompact:

1. **Oscillation**: energy escaping to high frequencies. The sequence
   $\sin(n\pi x)$ has constant $L^2$ norm but no convergent subsequence,
   since successive terms stay distance $1/\sqrt{2}$ apart.

2. **Translation**: energy escaping to spatial infinity. A fixed bump
   $\varphi(x - n)$ sliding off to infinity has no convergent subsequence
   on $\mathbb{R}^d$, since the supports eventually become disjoint.

The $H^1$ bound kills oscillation: $\|u_n'\|_{L^2}$ bounded forces the
high-frequency Fourier coefficients to decay. The **bounded domain** kills
translation: there is nowhere for the mass to escape to. Both hypotheses
are essential. On $\mathbb{R}^d$ (unbounded domain), the embedding
$H^1(\mathbb{R}^d) \hookrightarrow L^2(\mathbb{R}^d)$ is **not** compact
because translation sequences defeat it. On a bounded domain without the
derivative bound, $L^2(\Omega) \hookrightarrow L^2(\Omega)$ is the
identity, which is not compact in infinite dimensions.

Rellich-Kondrachov is the Sobolev-space counterpart of the Arzelà-Ascoli
theorem. In Arzelà-Ascoli, equicontinuity prevents rapid spatial
oscillation; here, the $H^1$ bound prevents rapid *frequency* oscillation.
In both cases, a regularity condition suppresses one pathology and a
bounded domain suppresses the other. Together they force approximate
finite-dimensionality.

### Connection to compact operators

In the language of the compact operators chapter
({prf:ref}`def-compact-operator`), the embedding
$\iota : H^1(\Omega) \hookrightarrow L^2(\Omega)$ **is** a compact
operator: it maps the bounded $H^1$ unit ball to a precompact subset of
$L^2$. This is why compact embeddings and compact operators are
interchangeable language.

The payoff for PDE is that compact embeddings upgrade weak convergence to
strong convergence, which is essential for passing to the limit through
nonlinearities. See the applications chapter for the full development:
the weak formulation via Lax-Milgram ({prf:ref}`lax-milgram`) and the
nonlinear PDE example ({prf:ref}`nonlinear-pde-tools`) both rely on
Rellich-Kondrachov as a critical step.


