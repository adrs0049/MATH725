---
kernelspec:
  name: python3
  display_name: Python 3
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/sobolev.pdf
    id: distributions-sobolev-pdf
downloads:
  - id: distributions-sobolev-pdf
    title: Download PDF
---

# Sobolev Spaces

:::{tip} Big Idea
$L^p$ norms measure height and width but are blind to oscillation. A function
can oscillate faster and faster while its $L^p$ norm stays constant. Sobolev
norms add a third dimension, **frequency**, by penalizing derivatives. The
Sobolev space $W^{k,p}(\Omega)$ consists of functions whose weak derivatives
up to order $k$ are in $L^p$: it sees not just how big a function is, but
how fast it oscillates.
:::


## From weak derivatives to function spaces

In the previous sections we defined the weak derivative of a locally integrable
function: $v = D^\alpha u$ weakly if

$$\int_\Omega u \, D^\alpha \varphi \, dx = (-1)^{|\alpha|} \int_\Omega v \, \varphi \, dx \quad \text{for all } \varphi \in C_c^\infty(\Omega).$$

This makes sense for any $u \in L^1_{\mathrm{loc}}(\Omega)$, but the derivative
$v$ might not be in $L^p$, or might not exist as an $L^p$ function at all.
Sobolev spaces are defined by requiring that weak derivatives exist **and** have
controlled size.

```{prf:definition} Sobolev space $W^{k,p}(\Omega)$
:label: def-sobolev-space

Let $\Omega \subseteq \mathbb{R}^d$ be open, $k \geq 0$ an integer, and $1
\leq p \leq \infty$. The **Sobolev space** $W^{k,p}(\Omega)$ consists of all
functions $u \in L^p(\Omega)$ whose weak derivatives $D^\alpha u$ exist and
belong to $L^p(\Omega)$ for all multi-indices $|\alpha| \leq k$. The
**Sobolev norm** is, for $1 \leq p < \infty$,

$$\|u\|_{W^{k,p}} = \left( \sum_{|\alpha| \leq k} \|D^\alpha u\|_{L^p(\Omega)}^p \right)^{1/p},$$

and for $p = \infty$,

$$\|u\|_{W^{k,\infty}} = \max_{|\alpha| \leq k} \|D^\alpha u\|_{L^\infty(\Omega)}.$$
```

```{prf:proposition} $W^{k,p}(\Omega)$ is a Banach space
:label: sobolev-banach

For $1 \leq p \leq \infty$ and $k \geq 0$, the space $(W^{k,p}(\Omega),
\|\cdot\|_{W^{k,p}})$ is a Banach space.
```

````{prf:proof}
:class: dropdown

Let $(u_n)$ be Cauchy in $W^{k,p}$. Then for each $|\alpha| \leq k$, the
sequence $(D^\alpha u_n)$ is Cauchy in $L^p(\Omega)$. Since $L^p$ is complete,
$D^\alpha u_n \to v_\alpha$ in $L^p$ for some $v_\alpha$. In particular,
$u_n \to v_0 =: u$ in $L^p$.

We verify that $v_\alpha = D^\alpha u$ weakly: for any $\varphi \in
C_c^\infty(\Omega)$,

$$\int_\Omega v_\alpha \, \varphi \, dx = \lim_n \int_\Omega D^\alpha u_n \, \varphi \, dx = \lim_n (-1)^{|\alpha|} \int_\Omega u_n \, D^\alpha \varphi \, dx = (-1)^{|\alpha|} \int_\Omega u \, D^\alpha \varphi \, dx.$$

So $u \in W^{k,p}$ and $u_n \to u$ in $W^{k,p}$.
````

The completeness proof is simple because it reduces to the completeness of
$L^p$: each derivative converges separately, and the weak derivative structure
is preserved under $L^p$ limits. This is a common pattern: Sobolev spaces
inherit their analytical properties from $L^p$.

```{prf:definition} The Hilbert-Sobolev spaces $H^k(\Omega)$
:label: def-hilbert-sobolev

For $p = 2$, the Sobolev space $W^{k,2}(\Omega)$ is denoted $H^k(\Omega)$.
It is a **Hilbert space** with inner product

$$\langle u, v \rangle_{H^k} = \sum_{|\alpha| \leq k} \int_\Omega D^\alpha u \cdot D^\alpha v \, dx.$$
```

The notation $H^k$ reflects the Hilbert space structure. For PDE applications,
$H^1(\Omega)$ is the most important space: it controls the function and its
first derivatives in $L^2$.


## What does the Sobolev norm measure?

In the introduction ({prf:ref}`rem-lp-interpretation`), we asked "what do $L^p$
norms measure?" and found that they capture two features of a function:

- **Height** (amplitude): the peak value, controlled by $L^\infty$.
- **Width** (spatial extent): the size of the support, contributing to $L^p$
  for $p < \infty$.

But these two features miss something fundamental. Consider the sequence
$u_n(t) = \sin(n\pi t)$ on $[0,1]$:

$$\|u_n\|_{L^2}^2 = \int_0^1 \sin^2(n\pi t) \, dt = \frac{1}{2} \quad \text{for all } n.$$

Every function in this sequence has the same height, the same support, and
the same $L^2$ norm, yet they are clearly different: $u_{100}$ oscillates
100 times faster than $u_1$. The $L^2$ norm is completely blind to this.

This is the same sequence that appeared in the weak convergence chapter
({prf:ref}`weak-not-strong-L2`): $\sin(n\pi t) \rightharpoonup 0$ weakly
in $L^2$, but $\|\sin(n\pi t)\|_{L^2} = 1/\sqrt{2}$ for all $n$. The $L^2$
norm cannot distinguish rapid oscillation from no oscillation at all.

```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import matplotlib.pyplot as plt

fig, axes = plt.subplots(1, 3, figsize=(15, 4.5))
t = np.linspace(0, 1, 1000)

# --- Panel 1: sin(nπt) for increasing n ---
ax = axes[0]
for n, color in [(1, 'C0'), (3, 'C1'), (10, 'C2'), (30, 'C4')]:
    ax.plot(t, np.sin(n * np.pi * t), color=color, lw=1.2, alpha=0.8,
            label=rf'$\sin({n}\pi t)$')
ax.set_xlabel(r'$t$', fontsize=11)
ax.set_ylabel(r'$u_n(t)$', fontsize=11)
ax.set_title('Same $L^2$ norm, different frequencies', fontsize=11)
ax.legend(fontsize=8, loc='upper right')
ax.tick_params(labelsize=9)

# --- Panel 2: L2 norm vs H1 norm ---
ax = axes[1]
ns = np.arange(1, 31)
l2_norms = np.ones_like(ns, dtype=float) / np.sqrt(2)
h1_norms = np.sqrt(0.5 + 0.5 * (ns * np.pi)**2)
ax.plot(ns, l2_norms, 'C0o-', ms=4, lw=1.5, label=r'$\|u_n\|_{L^2}$')
ax.plot(ns, h1_norms, 'C3s-', ms=4, lw=1.5, label=r'$\|u_n\|_{H^1}$')
ax.set_xlabel(r'$n$', fontsize=11)
ax.set_ylabel('Norm', fontsize=11)
ax.set_title(r'$L^2$ blind to frequency; $H^1$ sees it', fontsize=11)
ax.legend(fontsize=9)
ax.set_yscale('log')
ax.tick_params(labelsize=9)

# --- Panel 3: Fourier weights ---
ax = axes[2]
freqs = np.arange(0, 20)
for s, color, label in [(0, 'C0', '$s=0$ ($L^2$)'),
                         (1, 'C1', '$s=1$ ($H^1$)'),
                         (2, 'C3', '$s=2$ ($H^2$)')]:
    weights = (1 + freqs**2)**s
    ax.plot(freqs, weights, 'o-', color=color, ms=5, lw=1.5, label=label)
ax.set_xlabel(r'Frequency $|n|$', fontsize=11)
ax.set_ylabel(r'Weight $(1 + n^2)^s$', fontsize=11)
ax.set_title(r'Sobolev weights penalize high frequencies', fontsize=11)
ax.legend(fontsize=9)
ax.set_yscale('log')
ax.tick_params(labelsize=9)

plt.tight_layout()
plt.show()
```

*Left: the functions $\sin(n\pi t)$ oscillate faster but have constant $L^2$
norm. Center: the $L^2$ norm (blue) stays flat while the $H^1$ norm (red)
grows linearly in $n$, showing that the derivative detects oscillation. Right: the
Fourier weights $(1 + n^2)^s$ that define $H^s$; higher $s$ penalizes high
frequencies more aggressively.*

### The third feature: frequency

The Sobolev norm adds the missing dimension. Computing the derivative:

$$u_n'(t) = n\pi \cos(n\pi t), \qquad \|u_n'\|_{L^2}^2 = n^2\pi^2 \int_0^1 \cos^2(n\pi t) \, dt = \frac{n^2\pi^2}{2}.$$

So the $H^1$ norm sees the oscillation:

$$\|u_n\|_{H^1}^2 = \|u_n\|_{L^2}^2 + \|u_n'\|_{L^2}^2 = \frac{1}{2} + \frac{n^2\pi^2}{2} \to \infty.$$

The derivative term $\|u_n'\|_{L^2}$ blows up like $n\pi$: differentiation
converts oscillation frequency into amplitude. The $H^1$ norm detects the
frequency because derivatives penalize oscillation.

### The bump function scaling heuristic

Following Tao, we can make this precise with a model function that independently
controls all three features. Fix a bump function $\phi \in C_c^\infty(\mathbb{R})$
with $\operatorname{supp}(\phi) \subset [-1, 1]$, and consider

$$f_{A, R, N}(x) = A \, \phi(x/R) \, \sin(Nx)$$

where:
- $A > 0$ controls the **height** (amplitude),
- $R > 0$ controls the **width** (spatial extent: support $\approx [-R, R]$),
- $N > 0$ controls the **frequency** (oscillation rate).

The $L^p$ norm scales as (by the change of variables $y = x/R$):

$$\|f_{A,R,N}\|_{L^p}^p = \int |A \, \phi(x/R) \, \sin(Nx)|^p \, dx \approx A^p \, R \, \|\phi \cdot \sin\|_p^p$$

so $\|f_{A,R,N}\|_{L^p} \approx A \, R^{1/p}$. The frequency $N$ does **not
appear**: the $L^p$ norm is blind to oscillation.

The $W^{s,p}$ norm behaves differently. Each derivative of $\sin(Nx)$ pulls
down a factor of $N$:

$$D^s [A\,\phi(x/R)\,\sin(Nx)] \approx A \, N^s \, \phi(x/R) \, \sin(Nx + s\pi/2) + \text{lower-order terms}$$

(the lower-order terms involve derivatives of $\phi$, which contribute factors
of $R^{-1}$ instead of $N$, and are negligible when $N \gg 1/R$). Therefore:

$$\|f_{A,R,N}\|_{W^{s,p}} \approx A \, R^{1/p} \, N^s.$$

The three parameters are now visible:

| Norm | Scaling | What it sees |
|---|---|---|
| $\|f\|_{L^p}$ | $A \, R^{1/p}$ | Height $\times$ Width |
| $\|f\|_{W^{s,p}}$ | $A \, R^{1/p} \, N^s$ | Height $\times$ Width $\times$ Frequency$^s$ |

The extra factor $N^s$ is the whole point: **the Sobolev norm penalizes
high-frequency oscillation, with the penalty growing as $N^s$**. Higher
Sobolev index $s$ means stronger frequency penalty.

```{prf:remark} The three dimensions of function behavior
:label: three-dimensions-function
:class: dropdown

A function's "size" in the broad sense has three independent components:

1. **Amplitude** $A$: how tall is the function? (Controlled by $L^\infty$.)
2. **Spatial extent** $R$: how wide is the support? (Controlled by $L^p$ for $p < \infty$.)
3. **Frequency scale** $N$: how fast does it oscillate? (Controlled by $W^{s,p}$.)

$L^p$ norms see dimensions 1 and 2. Sobolev norms see all three. This is
why Sobolev spaces are the natural setting for PDE: differential equations
involve derivatives, and the Sobolev norm is the norm that controls derivatives.
```

### Regularity as frequency decay

The bump function heuristic shows that the Sobolev norm penalizes high
frequency. But how many degrees of regularity does a function have? To
make this precise, consider the one-parameter family

$$G_{s,N}(x) = N^{-s}\,\phi(x)\,\sin(Nx), \qquad s > 0, \quad N \gg 1,$$

where $\phi \in C_c^\infty(\mathbb{R})$ is a fixed bump. The prefactor
$N^{-s}$ is chosen so that $\|G_{s,N}\|_{W^{s,p}}$ remains bounded as
$N \to \infty$ (from the scaling $\|f_{A,R,N}\|_{W^{s,p}} \approx A
R^{1/p} N^s$ with $A = N^{-s}$ and $R = 1$).

Computing derivatives (keeping only the dominant term when $N \gg 1$):

$$G_{s,N}^{(k)}(x) \approx N^{k-s}\,\phi(x)\,\sin(Nx + k\pi/2) + \text{lower-order terms}.$$

The behavior splits sharply at $k = s$:

| Derivative order $k$ | $\|G_{s,N}^{(k)}\|_{L^p}$ as $N \to \infty$ | Interpretation |
|---|---|---|
| $k < s$ | $\to 0$ (decays as $N^{k-s}$) | Well within regularity budget |
| $k = s$ | $O(1)$ (bounded) | Exactly at the regularity threshold |
| $k > s$ | $\to \infty$ (grows as $N^{k-s}$) | Beyond the regularity budget |

The following plot shows $G_{s,N}$ for $s = 2$ and increasing $N$. The
function itself shrinks (because of the $N^{-s}$ prefactor), but its second
derivative stays $O(1)$ and its third derivative grows.

```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(-1.5, 1.5, 4000)
dx = x[1] - x[0]

def bump(x):
    """Smooth bump function supported on [-1, 1]."""
    result = np.zeros_like(x)
    mask = np.abs(x) < 1
    result[mask] = np.exp(-1 / (1 - x[mask]**2))
    return result / np.max(result)

s = 2  # regularity index
Ns = [5, 15, 50]
phi = bump(x)

fig, axes = plt.subplots(1, 3, figsize=(12, 3.5))
titles = [
    '$G_{2,N}(x)$  (k=0 < s)',
    "$G_{2,N}''(x)$  (k=2 = s)",
    "$G_{2,N}'''(x)$  (k=3 > s)",
]
deriv_orders = [0, 2, 3]

for col, (k, title) in enumerate(zip(deriv_orders, titles)):
    ax = axes[col]
    for N in Ns:
        g = N**(-s) * phi * np.sin(N * x)
        # Compute k-th derivative numerically
        gk = g.copy()
        for _ in range(k):
            gk = np.gradient(gk, dx)
        lp_norm = np.sqrt(np.trapezoid(gk**2, x))
        ax.plot(x, gk, lw=1.0, label=f'$N={N}$, $\\|\\cdot\\|_2={lp_norm:.2f}$')
    ax.set_title(title, fontsize=10)
    ax.set_xlabel('$x$')
    ax.legend(fontsize=7)
    ax.axhline(0, color='gray', lw=0.5, zorder=0)
    ax.grid(True, alpha=0.3)

fig.suptitle('Regularity threshold for $G_{s,N}$ with $s=2$: '
             '$L^2$ norms decay ($k<s$), stay bounded ($k=s$), or blow up ($k>s$)',
             fontsize=10, y=1.02)
plt.tight_layout()
plt.show()
```

```{prf:remark} Sobolev regularity is sharp
:label: sobolev-regularity-sharp
:class: dropdown

The family $G_{s,N}$ demonstrates that **$s$ is a sharp regularity
threshold**: the function has exactly $s$ derivatives in $L^p$ and no more.
This is the core idea of the Sobolev scale: the index $s$ counts exactly
how many derivatives a function can afford.

The mechanism is frequency: each derivative pulls down a factor of $N$,
and the prefactor $N^{-s}$ budgets exactly $s$ such factors before the
$L^p$ norm diverges.
```


### The Fourier picture

For $H^s = W^{s,2}$ on the torus $[0, 2\pi]$ (or $\mathbb{R}^d$ via the
Fourier transform), the connection to frequency is exact. If $u(x) =
\sum_n \hat{u}_n \, e^{inx}$, then $D^s u$ has Fourier coefficients
$(in)^s \hat{u}_n$, and Parseval gives:

$$\|u\|_{H^s}^2 = \sum_n (1 + |n|^2)^s |\hat{u}_n|^2.$$

The weight $(1 + |n|^2)^s$ penalizes high frequencies $|n|$ by a factor of
$|n|^{2s}$. This makes the frequency interpretation precise:

- **$L^2$ ($s = 0$):** all frequencies weighted equally. The norm is
  $\sum |\hat{u}_n|^2$: total energy, regardless of frequency.
- **$H^1$ ($s = 1$):** weight $(1 + n^2)$. High frequencies are penalized
  quadratically.
- **$H^k$ ($s = k$):** weight $(1 + n^2)^k$. Higher $k$ means stronger
  suppression of high frequencies.

A function is in $H^s$ if and only if its Fourier coefficients decay fast
enough to compensate for the weight $(1 + |n|^2)^s$. Smoother functions
have faster-decaying Fourier coefficients, so they live in higher Sobolev
spaces.


## Examples: what is and isn't in $W^{1,2}$

```{prf:example} Functions in and out of $H^1$
:label: sobolev-membership-examples

**In $H^1(0,1)$:**

- Any $C^1$ function on $[0,1]$: classical derivatives are in $L^2$.
- $f(x) = |x - 1/2|$: the weak derivative is $f'(x) = \operatorname{sgn}(x - 1/2)$,
  which is in $L^2$ (in fact in $L^\infty$). The kink at $x = 1/2$ is
  invisible to the $H^1$ norm.

**Not in $H^1(0,1)$:**

- The Heaviside function $H(x) = \mathbf{1}_{[1/2, 1]}(x)$: its weak
  derivative is $\delta_{1/2}$, a measure and not an $L^2$ function. So
  $H \in L^2$ but $H \notin H^1$. The jump discontinuity is detected by
  the Sobolev norm.
- $f(x) = x^{-1/4}$ on $(0,1)$: $f \in L^2(0,1)$ (barely), but
  $f'(x) = -\frac{1}{4}x^{-5/4} \notin L^2(0,1)$. The singularity at
  $0$ is too strong for one derivative in $L^2$.

**The pattern:** $H^1$ tolerates kinks (Lipschitz singularities) but not
jumps or blowup. This is because the weak derivative of a Lipschitz function
is bounded (hence in every $L^p$), while the derivative of a discontinuous
function is a measure.
```


