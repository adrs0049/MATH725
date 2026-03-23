---
kernelspec:
  name: python3
  display_name: Python 3
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/weak-convergence.pdf
    id: duality-weak-convergence-pdf
downloads:
  - id: duality-weak-convergence-pdf
    title: Download PDF
---

# Weak and Weak* Convergence

:::{tip} Big Idea
In infinite-dimensional spaces, the unit ball is **never compact** in the norm
topology. This is a serious obstruction: we cannot extract
convergent subsequences from bounded sequences, which is the workhorse of
existence proofs in finite dimensions. Weak topologies fix this. By testing
convergence against linear functionals rather than measuring distances directly,
we get a coarser topology in which bounded sets **are** compact:

- **Banach-Alaoglu**: the unit ball of $X^*$ is compact in the weak\* topology.
- **Eberlein-Šmulian**: for subsets of a Banach space in the weak topology,
  compactness, sequential compactness, and limit point compactness are all
  equivalent.

In a **reflexive** space, Banach-Alaoglu (applied via $X \cong X^{**}$) makes
the unit ball weakly compact, and Eberlein-Šmulian upgrades this to sequential
compactness: every bounded sequence has a weakly convergent subsequence.
:::

With the Hahn-Banach theorem in hand, we know that $X^*$ is rich enough to
separate points and recover the norm. This opens the door to new notions of
convergence that are weaker than norm convergence but powerful enough for
applications, particularly in PDE and the calculus of variations.

Recall the **foliation picture** from the previous sections: each functional $f
\in X^*$ slices $X$ into parallel level sets, assigning a reading $f(x)$ to each
point. We can think of each foliation as a **measuring instrument** (following
Hillen and Bollobas): $f_1$ measures "temperature," $f_2$ measures "weight,"
$f_3$ measures "color," and so on. The level sets of $f$ are the iso-measurement
surfaces, like isotherms on a weather map. Crucially, these are **linear
measuring instruments**: each $f \in X^*$ respects the linear structure of $X$,
so the reading of a superposition is the superposition of readings, $f(\alpha x +
\beta y) = \alpha f(x) + \beta f(y)$. This is what the Hahn-Banach theorem
provides — not just *any* way to tell points apart, but a supply of *linear*
instruments rich enough to form a **complete measurement system**: if two objects
give the same reading on every linear instrument, they are the same object.

The question now becomes: what does it mean for a sequence of objects (or a
sequence of instruments) to "converge"?


## Strong Convergence (Norm Convergence)

```{prf:definition} Strong convergence
:label: strong-convergence-def

Let $X$ be a normed space and let $(x_n)_{n \geq 1}$ be a sequence in $X$. We say $x_n \to x$ **strongly** (or **in norm**) if

$$\|x_n - x\| \to 0 \quad \text{as } n \to \infty.$$
```

This is the familiar notion: the points $x_n$ physically move toward $x$, and
the distance $\|x_n - x\|$ shrinks to zero. Since $|f(x_n) - f(x)| \leq \|f\|
\cdot \|x_n - x\|$, strong convergence forces all instrument readings to
converge uniformly over $\|f\| \leq 1$. But it is defined by the norm directly,
not by the instruments.

```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import matplotlib.pyplot as plt
from matplotlib.patches import Circle

fig, ax = plt.subplots(1, 1, figsize=(6, 6))

# Target point
x = np.array([1.0, 0.5])
ax.plot(*x, 'C3o', ms=10, zorder=10)
ax.text(x[0] + 0.1, x[1] + 0.1, r'$x$', fontsize=14, color='C3', fontweight='bold')

# Points spiraling in toward x
np.random.seed(42)
N = 12
radii = np.linspace(1.2, 0.08, N)
angles = np.linspace(0, 4 * np.pi, N)
for i in range(N):
    pt = x + radii[i] * np.array([np.cos(angles[i]), np.sin(angles[i])])
    color_val = i / N
    ax.plot(*pt, 'o', color=plt.cm.viridis(color_val), ms=6, zorder=5)
    if i < 4 or i == N - 1:
        label = f'$x_{{{i+1}}}$'
        ax.text(pt[0] + 0.08, pt[1] + 0.08, label, fontsize=9,
                color=plt.cm.viridis(color_val))

# Draw shrinking circles to show convergence
for r in [1.2, 0.7, 0.3]:
    circle = Circle(x, r, fill=False, edgecolor='gray', lw=0.8, ls='--', alpha=0.4)
    ax.add_patch(circle)

# Draw a foliation in the background
for c in np.arange(-2, 4, 0.5):
    t = np.linspace(-1, 3.5, 100)
    # f(u,v) = u + v = c
    ax.plot(t, c - t, 'gray', alpha=0.12, lw=0.7)

ax.set_xlim(-0.8, 3.0)
ax.set_ylim(-1.2, 2.5)
ax.set_aspect('equal')
ax.set_title('Strong convergence: points cluster toward $x$', fontsize=12)
ax.set_xlabel(r'$x_1$')
ax.set_ylabel(r'$x_2$')
plt.tight_layout()
plt.show()
```


## Weak Convergence

```{prf:definition} Weak convergence
:label: weak-convergence-def

Let $X$ be a normed space and let $(x_n)_{n \geq 1}$ be a sequence in $X$. We say $x_n \rightharpoonup x$ **weakly** if

$$f(x_n) \to f(x) \quad \text{for every } f \in X^*.$$
```

Each instrument $f$ foliates $X$ into level sets $\{x : f(x) = c\}$, the
"isotherms" for that measurement. Weak convergence means: in every foliation,
the readings $f(x_n)$ settle down to $f(x)$. The objects $x_n$ need not become
close to $x$; they can keep bouncing around, as long as every instrument
eventually reads the same value as it does on $x$.

```{prf:example} Weak but not strong convergence in $L^2$
:label: weak-not-strong-L2

In $L^2([0,1])$, the sequence $x_n = \sin(n\pi t)$ converges weakly to $0$, but
**not** strongly. Each $x_n$ has norm $\|x_n\|_{L^2} = 1/\sqrt{2}$, so the
sequence stays on a sphere. But for any $g \in L^2$,
the Riemann-Lebesgue lemma gives:

$$\int_0^1 g(t)\sin(n\pi t)\,dt \to 0 \quad \text{as } n \to \infty$$

so $f_g(x_n) \to 0$ for every functional $f_g \in (L^2)^*$, i.e., $x_n \rightharpoonup 0$.
```

```{prf:remark} Pointwise vs. uniform convergence over the dual
:label: weak-strong-gap-remark
:class: dropdown

Why does weak convergence not imply strong convergence? After all, weak
convergence requires $\langle g, x_n \rangle \to 0$ for **all** $g \in L^2$
— isn't "all" a strong demand?

The key is that weak convergence is **pointwise in $g$**: we fix $g$ first,
then send $n \to \infty$. For any fixed $g$, the Fourier coefficients
$\langle g, \sin(n\pi t) \rangle = \hat{g}(n) \to 0$ because the tail of a
square-summable series vanishes. Each instrument eventually loses track of the
oscillation.

But we are free to **change the instrument with $n$**. Choose $g_n = \sin(n\pi
t)$, i.e., the instrument that is perfectly aligned with $x_n$. Then

$$\langle g_n, x_n \rangle = \|\sin(n\pi t)\|_{L^2}^2 = \frac{1}{2}$$

for every $n$ — this "adaptive" instrument always catches the oscillation. The
supremum over the unit ball,

$$\sup_{\|g\| \leq 1} |\langle g, x_n \rangle| = \|x_n\| = \frac{1}{\sqrt{2}},$$

never decays. But this supremum **is** the norm of $x_n$, and driving it to
zero would be exactly strong convergence.

Why is this not a problem for weak convergence? Because the definition
({prf:ref}`weak-convergence-def`) quantifies as: *for every fixed $g \in X^*$,
$\langle g, x_n \rangle \to 0$*. The functional $g$ is chosen **once and for
all**, and then we ask whether the sequence of numbers $\langle g, x_n \rangle$
converges. An adaptive choice $g_n$ that changes with $n$ does not define a
single sequence of real numbers — it defines a different measurement at each
step. This is not what any individual instrument reads; it is a meta-observation
assembled by switching instruments. No single linear measuring instrument in
$X^*$ witnesses the non-convergence.

So the gap between weak and strong convergence is precisely the gap between
**pointwise** and **uniform** convergence over $X^*$: each fixed linear
instrument eventually stops detecting the oscillation, but the worst-case
instrument shifts with $n$ to stay aligned with $x_n$.

The identity $\sup_{\|g\| \leq 1} |\langle g, x_n \rangle| = \|x_n\|$ is a
consequence of the Hahn-Banach theorem: for any $x \in X$, there exists a
**norming functional** $g_x \in X^*$ with $\|g_x\| = 1$ and $g_x(x) =
\|x\|$. So the supremum over the unit ball of $X^*$ is always attained (or
approached, in the non-reflexive case), and equals the norm. In other words,
the norm of $x$ is exactly the largest reading that any unit-norm linear
instrument can produce on $x$.

This is also where the Banach-Steinhaus theorem ({prf:ref}`banach-steinhaus`)
enters: weak convergence $x_n \rightharpoonup x$ implies that $\langle g, x_n
\rangle$ is bounded for each fixed $g$. Each $x_n$ acts as a bounded linear
functional on $X^*$ via evaluation, $x_n(g) = g(x_n)$, and the family
$\{x_n\}$ is pointwise bounded on $X^*$. The uniform boundedness principle then
gives $\sup_n \|x_n\| < \infty$. So weak convergence automatically implies
norm-boundedness — but not norm-convergence.
```

```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import matplotlib.pyplot as plt

fig, axes = plt.subplots(1, 3, figsize=(15, 4.5))

t = np.linspace(0, 1, 500)

# --- Panel 1: The functions sin(nπt) ---
ax = axes[0]
for n, color in [(1, 'C0'), (3, 'C1'), (7, 'C2'), (15, 'C4')]:
    ax.plot(t, np.sin(n * np.pi * t), color=color, lw=1.5, alpha=0.8,
            label=rf'$\sin({n}\pi t)$')
ax.axhline(0, color='C3', lw=2.5, ls='-', alpha=0.7, label=r'limit $x = 0$')
ax.set_xlabel(r'$t$', fontsize=11)
ax.set_ylabel(r'$x_n(t)$', fontsize=11)
ax.set_title('The sequence: oscillates, never settles', fontsize=11)
ax.legend(fontsize=8, loc='upper right')
ax.tick_params(labelsize=9)

# --- Panel 2: ||x_n|| stays constant ---
ax = axes[1]
ns = np.arange(1, 21)
norms = np.ones_like(ns, dtype=float) / np.sqrt(2)
ax.plot(ns, norms, 'C3o-', ms=5, lw=1.5)
ax.axhline(1/np.sqrt(2), color='C3', ls='--', alpha=0.4)
ax.axhline(0, color='gray', ls='-', alpha=0.3)
ax.set_xlabel(r'$n$', fontsize=11)
ax.set_ylabel(r'$\|x_n\|_{L^2}$', fontsize=11)
ax.set_title(rf'Norm: $\|x_n\| = 1/\sqrt{{2}}$ (no convergence to 0)', fontsize=11)
ax.set_ylim(-0.1, 1.0)
ax.tick_params(labelsize=9)

# --- Panel 3: Inner products with several g decay to 0 ---
ax = axes[2]
test_funcs = [
    (lambda t: np.ones_like(t), r'$g = 1$', 'C0'),
    (lambda t: t, r'$g = t$', 'C1'),
    (lambda t: np.cos(2*np.pi*t), r'$g = \cos(2\pi t)$', 'C2'),
    (lambda t: np.where(t < 0.5, 1.0, -1.0), r'$g = \mathrm{sgn}(t-1/2)$', 'C4'),
]

ns = np.arange(1, 26)
dt = t[1] - t[0]
for g_func, label, color in test_funcs:
    g_vals = g_func(t)
    inner_prods = [np.sum(g_vals * np.sin(n * np.pi * t)) * dt for n in ns]
    ax.plot(ns, inner_prods, 'o-', color=color, ms=4, lw=1.2, label=label)

ax.axhline(0, color='gray', ls='-', alpha=0.3)
ax.set_xlabel(r'$n$', fontsize=11)
ax.set_ylabel(r'$\langle g, x_n \rangle$', fontsize=11)
ax.set_title(r'Every foliation height $\to 0$: weak convergence', fontsize=11)
ax.legend(fontsize=8, loc='upper right')
ax.tick_params(labelsize=9)

plt.tight_layout()
plt.show()
```

*Left: the functions $\sin(n\pi t)$ oscillate faster and faster, never settling
down pointwise. Center: the $L^2$ norm stays at $1/\sqrt{2}$ for every $n$, so
the sequence does not converge strongly. Right: the inner product $\langle g,
x_n \rangle$ decays to $0$ for every test function $g \in L^2$, no matter its
shape. Every "foliation height" converges, even though the functions themselves
keep bouncing around. This is weak convergence without strong convergence.*

### The foliation picture of weak convergence

Each functional $g \in L^2$ defines a foliation of $L^2$ into parallel
hyperplanes $\{x : \langle g, x \rangle = c\}$. Weak convergence $x_n
\rightharpoonup 0$ means that in *every* foliation, the heights $\langle g, x_n
\rangle$ converge to $0$. The points $x_n$ jump between different hyperplanes in
each foliation, but eventually the heights settle near the origin's level set.

```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import matplotlib.pyplot as plt

# Compute actual inner products for sin(nπt) against several g
t = np.linspace(0, 1, 1000)
dt = t[1] - t[0]
ns_all = np.arange(1, 16)

test_funcs = [
    (np.ones_like(t), r'$g_1 = 1$'),
    (t, r'$g_2 = t$'),
    (np.cos(2*np.pi*t), r'$g_3 = \cos(2\pi t)$'),
]

# Compute heights for each functional
heights = {}
for g_vals, label in test_funcs:
    heights[label] = [np.sum(g_vals * np.sin(n * np.pi * t)) * dt for n in ns_all]

fig, axes = plt.subplots(1, 3, figsize=(15, 5))
colors_pts = plt.cm.viridis(np.linspace(0.1, 0.9, len(ns_all)))

for idx, (g_vals, label) in enumerate(test_funcs):
    ax = axes[idx]
    h = heights[label]

    # Draw the foliation: horizontal lines representing level sets of g
    for c in np.arange(-0.8, 0.9, 0.1):
        alpha = 0.5 if abs(c) < 0.005 else 0.12
        lw_val = 2.0 if abs(c) < 0.005 else 0.6
        ax.axhline(c, color='gray', alpha=alpha, lw=lw_val)

    # The zero level set (the kernel) highlighted
    ax.axhline(0, color='C0', lw=2, alpha=0.6, label=r'$\langle g, 0 \rangle = 0$')

    # Plot each x_n as a point at its height in this foliation
    for i, n in enumerate(ns_all):
        ax.plot(n, h[i], 'o', color=colors_pts[i], ms=7, zorder=5)

    # Connect with a line to show the trajectory
    ax.plot(ns_all, h, '-', color='C4', alpha=0.4, lw=1)

    # Shade the band near 0 to show convergence
    ax.axhspan(-0.05, 0.05, color='C0', alpha=0.08)

    ax.set_xlabel(r'$n$', fontsize=11)
    ax.set_ylabel(r'height $\langle g, x_n \rangle$', fontsize=11)
    ax.set_title(f'Foliation by {label}', fontsize=11)
    ax.legend(fontsize=9, loc='upper right')
    ax.set_ylim(-0.8, 0.8)
    ax.tick_params(labelsize=9)

plt.suptitle(r'Weak convergence of $\sin(n\pi t) \rightharpoonup 0$: heights settle to $0$ in every foliation',
             fontsize=12, y=1.02)
plt.tight_layout()
plt.show()
```

*Each panel is a different foliation of $L^2$, defined by a functional $g$. The
vertical axis is the "height" $\langle g, x_n \rangle$ that the foliation
assigns to $x_n = \sin(n\pi t)$. The points jump around between level sets, but
in every foliation the heights converge to $0$ (the blue line). The sequence
never converges in norm, yet every foliation eventually reads near-zero heights.
This is weak convergence.*

:::{admonition} Strong vs. Weak
:class: important

Strong convergence means the objects cluster in space. Weak convergence means
every instrument reading converges, even though the objects may keep moving. The
gap is real: $\sin(n\pi x) \rightharpoonup 0$ but $\|\sin(n\pi x)\| = 1/\sqrt{2}
\not\to 0$.

In finite dimensions, this gap **disappears**: weak and strong convergence are
equivalent (finitely many instruments suffice to control the norm). The gap is
an essentially infinite-dimensional phenomenon.
:::


### Basic properties of weak convergence

```{prf:proposition} Weak limits are unique
:label: weak-limits-unique

Let $X$ be a normed space. If $x_n \rightharpoonup x$ and $x_n \rightharpoonup
y$, then $x = y$.
```

````{prf:proof}
:class: dropdown

For every $f \in X^*$, we have $f(x) = \lim f(x_n) = f(y)$, so $f(x - y) = 0$
for all $f \in X^*$. By the {prf:ref}`sup formula <hb-sup-formula>`, $\|x - y\|
= \sup_{\|f\| \leq 1} |f(x - y)| = 0$, so $x = y$.
````

```{prf:proposition} Weakly convergent sequences are bounded
:label: weak-convergence-bounded

Let $X$ be a Banach space. If $x_n \rightharpoonup x$, then $\sup_n \|x_n\| <
\infty$.
```

````{prf:proof}
:class: dropdown

Each $x_n$ defines an element $J[x_n] \in X^{**}$ by $J[x_n](f) = f(x_n)$.
Since $x_n \rightharpoonup x$, for each fixed $f \in X^*$ the sequence
$J[x_n](f) = f(x_n)$ converges and is therefore bounded. So the family
$\{J[x_n]\}_{n \geq 1} \subseteq X^{**}$ is pointwise bounded on $X^*$. Since
$X^*$ is a Banach space, the Banach-Steinhaus theorem
({prf:ref}`banach-steinhaus`) gives $\sup_n \|J[x_n]\|_{X^{**}} < \infty$. By
{prf:ref}`canonical-embedding-isometry`, $\|J[x_n]\|_{X^{**}} = \|x_n\|$, so
$\sup_n \|x_n\| < \infty$.
````

```{prf:proposition} Compact operators turn weak convergence into strong convergence
:label: compact-weak-to-strong

Let $X, Y$ be Banach spaces and $A : X \to Y$ a compact linear operator. If
$x_n \rightharpoonup x$ in $X$, then $Ax_n \to Ax$ strongly in $Y$.
```

````{prf:proof}
:class: dropdown

Since $x_n \rightharpoonup x$, {prf:ref}`weak-convergence-bounded` gives
$\sup_n \|x_n\| \leq C$. The sequence $(x_n - x)$ converges weakly to $0$ and
is bounded, so $(A(x_n - x))$ lies in the image of a bounded set under a
compact operator, hence its closure is compact in $Y$.

It suffices to show every subsequence of $(Ax_n)$ has a further subsequence
converging to $Ax$. Let $(x_{n_k})$ be any subsequence. Since $A$ is compact
and $(x_{n_k})$ is bounded, there exists a further subsequence $(x_{n_{k_j}})$
such that $Ax_{n_{k_j}} \to z$ for some $z \in Y$. We identify $z = Ax$: for
any $g \in Y^*$, the functional $f = g \circ A \in X^*$, so

$$g(Ax_{n_{k_j}}) = f(x_{n_{k_j}}) \to f(x) = g(Ax).$$

Since $Ax_{n_{k_j}} \to z$ strongly, also $g(Ax_{n_{k_j}}) \to g(z)$, giving
$g(z) = g(Ax)$ for all $g \in Y^*$. By Hahn-Banach, $z = Ax$.

Since every subsequence of $(Ax_n)$ has a further subsequence converging to
$Ax$, the full sequence converges: $Ax_n \to Ax$.
````


### Convergence in expectation as weak convergence

Why is $L^1$ the natural Banach space for probability? A random variable $X$ on
a probability space $(\Omega, \mathcal{F}, \mathbb{P})$ is an element of
$L^1(\Omega, \mathbb{P})$ precisely when it has **finite expectation**:
$\mathbb{E}[|X|] = \int_\Omega |X|\,d\mathbb{P} < \infty$. The $L^1$ norm *is*
the expected absolute value:

$$\|X\|_{L^1} = \mathbb{E}[|X|].$$

So $L^1(\Omega, \mathbb{P})$ is the space of "integrable random variables," and
its norm measures the average size of a random variable. This is the minimal
regularity needed to do expectation-based calculations.

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


## Weak* Convergence

```{prf:definition} Weak* convergence
:label: weak-star-convergence-def

Let $X$ be a normed space and let $(f_n)_{n \geq 1}$ be a sequence in $X^*$. We say $f_n \xrightarrow{w^*} f$ (**weak\* convergence**) if

$$f_n(x) \to f(x) \quad \text{for every } x \in X.$$
```

Now the picture flips: each $f_n$ *is* an instrument, and the sequence is a
sequence of instruments, not objects. Think of replacing your entire measurement
apparatus -- swapping one thermometer for another, one scale for another. Fix
any object $x$ and read off $f_1(x), f_2(x), f_3(x), \ldots$. Weak\* convergence
means these readings stabilize to $f(x)$ for every fixed object. Geometrically,
each $f_n$ defines a different foliation (different isotherms), and these
foliations rearrange from step to step, but at every fixed point the height
reading converges.

- **Weak:** fix the instrument, watch objects change -- readings stabilize.
- **Weak\*:** fix the object, watch instruments change -- readings stabilize.

```{prf:remark} Weak* vs. weak convergence in $X^*$
:label: weak-star-vs-weak-remark
:class: dropdown

A sequence $(f_n)$ in $X^*$ lives in a Banach space, so it has *two* notions of
non-norm convergence:

1. **Weak\* convergence** ($f_n \xrightarrow{w^*} f$): test against every $x \in
   X$, i.e., $f_n(x) \to f(x)$ for all $x \in X$.
2. **Weak convergence in $X^*$** ($f_n \rightharpoonup f$): test against every
   $\phi \in X^{**}$, i.e., $\phi(f_n) \to \phi(f)$ for all $\phi \in X^{**}$.

Since the canonical embedding $J \colon X \hookrightarrow X^{**}$ identifies
each $x \in X$ with the evaluation functional $J(x)(\cdot) = (\cdot)(x)$, every
element of $X$ gives rise to an element of $X^{**}$. So weak convergence in
$X^*$ (testing against all of $X^{**}$) automatically implies weak\* convergence
(testing against only the image of $X$ in $X^{**}$). **Weak\* is the weaker
notion**: it asks less, because it tests against fewer functionals.

In the instrument analogy: weak\* convergence validates the new instruments
$f_n$ by pointing them at **real objects** $x \in X$ — things we can hold in
our hand and measure. Weak convergence in $X^*$ additionally requires that the
instruments agree when probed by **abstract evaluation functionals** $\phi \in
X^{**} \setminus J(X)$, which do not correspond to any concrete object in $X$.
These are "measurements of instruments" that cannot be realized by pointing the
instrument at an actual object.

When $X$ is **reflexive** ($J$ is surjective, so $X = X^{**}$), every element
of $X^{**}$ comes from a real object, the abstract functionals disappear, and
weak\* and weak convergence in $X^*$ coincide. When $X$ is not reflexive, weak\*
convergence is strictly weaker — a sequence can stabilize on every real object
while still misbehaving on some abstract evaluation functional.
```


### Visualizing weak* convergence in $\mathbb{R}^2$

Consider $f_n(x,y) = (1 - 1/n)\,x + (1/n)\,y$ on $(\mathbb{R}^2,
\|\cdot\|_\infty)$. Each $f_n$ has kernel line $(1 - 1/n)x + (1/n)y = 0$, which
slowly rotates toward the $y$-axis as $n \to \infty$. For any fixed point $(a,
b)$:

$$f_n(a, b) = \left(1 - \frac{1}{n}\right)a + \frac{1}{n}b \to a = f(a, b)$$

where $f(x,y) = x$. The foliations converge pointwise: at each location, the
height readings stabilize, even though the kernel lines are visibly rotating
from picture to picture.

As with weak convergence, the $\mathbb{R}^2$ picture is a visual scaffold: in
finite dimensions weak\* = weak = strong, so the foliations converge uniformly,
not just pointwise. The genuine weak\* phenomenon -- where pointwise convergence
of height readings does not imply uniform convergence -- requires infinite
dimensions. The top row below shows the geometry (rotating level sets), but the
real content is in the bottom row: height readings at fixed test points
stabilizing one by one.

```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import matplotlib.pyplot as plt
from matplotlib.patches import Polygon

fig, axes = plt.subplots(2, 3, figsize=(15, 10))

# Top row: the foliations f_n for n = 2, 4, ∞
square_verts = np.array([[-1, -1], [1, -1], [1, 1], [-1, 1]])

# Fixed test points
test_points = [
    (1.5, 0.8, r'$p_1$', 'C3'),
    (-0.5, 1.2, r'$p_2$', 'C2'),
    (0.8, -0.6, r'$p_3$', 'C4'),
]

n_values = [2, 4, 1000]  # 1000 ≈ ∞
titles_top = [r'$f_2 = \frac{1}{2}x + \frac{1}{2}y$',
              r'$f_4 = \frac{3}{4}x + \frac{1}{4}y$',
              r'$f = x$ (limit)']

for idx, (n_val, title) in enumerate(zip(n_values, titles_top)):
    ax = axes[0, idx]

    a = 1 - 1/n_val
    b = 1/n_val

    # Draw unit square
    sq = Polygon(square_verts, fill=True, facecolor='C0', alpha=0.08,
                 edgecolor='C0', lw=1.5)
    ax.add_patch(sq)

    # Draw level sets
    t = np.linspace(-2.5, 2.5, 200)
    for level in np.arange(-3, 3.5, 0.5):
        if abs(b) > 1e-6:
            y_line = (level - a * t) / b
            mask = (y_line > -2.5) & (y_line < 2.5)
            lw = 1.5 if abs(level - round(level)) < 0.01 and level == int(level) else 0.6
            alpha_val = 0.5 if lw > 1 else 0.15
            color = 'C3' if abs(level) < 0.01 else 'gray'
            ax.plot(t[mask], y_line[mask], color=color, alpha=alpha_val, lw=lw)
        else:
            # Vertical lines
            if abs(a) > 1e-6:
                x_val = level / a
                if -2.5 < x_val < 2.5:
                    lw = 1.5 if abs(level - round(level)) < 0.01 and level == int(level) else 0.6
                    alpha_val = 0.5 if lw > 1 else 0.15
                    color = 'C3' if abs(level) < 0.01 else 'gray'
                    ax.axvline(x_val, color=color, alpha=alpha_val, lw=lw)

    # Plot test points with their heights
    for (px, py, label, color) in test_points:
        height = a * px + b * py
        ax.plot(px, py, 'o', color=color, ms=7, zorder=10)
        ax.text(px + 0.08, py + 0.12, f'{label}: {height:.2f}', fontsize=9, color=color)

    ax.set_xlim(-2.2, 2.2)
    ax.set_ylim(-2.2, 2.2)
    ax.set_aspect('equal')
    ax.set_title(title, fontsize=12)
    ax.set_xlabel(r'$x$')
    ax.set_ylabel(r'$y$')

# Bottom row: height readings at each test point as n varies
n_range = np.arange(2, 20)
for idx, (px, py, label, color) in enumerate(test_points):
    ax = axes[1, idx]
    heights = [(1 - 1/n) * px + (1/n) * py for n in n_range]
    limit = px  # f(x,y) = x

    ax.plot(n_range, heights, 'o-', color=color, ms=5, lw=1.5)
    ax.axhline(limit, color=color, ls='--', lw=2, alpha=0.6,
               label=f'limit $f({label[1:-1]}) = {limit}$')
    ax.set_xlabel(r'$n$')
    ax.set_ylabel(f'$f_n({label[1:-1]})$')
    ax.set_title(f'Height readings at {label}', fontsize=11)
    ax.legend(fontsize=9)
    ax.set_ylim(min(min(heights), limit) - 0.3, max(max(heights), limit) + 0.3)

plt.suptitle(r'Weak* convergence: foliations rotate, height readings stabilize at each point',
             fontsize=13, y=1.01)
plt.tight_layout()
plt.show()
```


## The Three Convergences Compared

```{prf:proposition} Strong convergence implies weak convergence
:label: strong-implies-weak

Let $X$ be a normed space. If $x_n \to x$ strongly, then $x_n \rightharpoonup x$
weakly.
```

````{prf:proof}
:class: dropdown

Let $f \in X^*$. Since $f$ is a bounded linear functional,

$$|f(x_n) - f(x)| = |f(x_n - x)| \leq \|f\| \cdot \|x_n - x\| \to 0.$$

Since $f$ was arbitrary, $x_n \rightharpoonup x$.
````

The converse is false in infinite dimensions: {prf:ref}`weak-not-strong-L2`
gives a sequence in $L^2$ with $x_n \rightharpoonup 0$ but $\|x_n\| =
1/\sqrt{2}$ for all $n$.

```{prf:proposition} Strong convergence in $X^*$ implies weak\* convergence
:label: strong-implies-weak-star

Let $X$ be a normed space. If $f_n \to f$ in the norm of $X^*$, then $f_n
\xrightarrow{w^*} f$.
```

````{prf:proof}
:class: dropdown

For any fixed $x \in X$,

$$|f_n(x) - f(x)| = |(f_n - f)(x)| \leq \|f_n - f\| \cdot \|x\| \to 0.$$

Since $x$ was arbitrary, $f_n \xrightarrow{w^*} f$.
````

```{prf:proposition} Weak convergence in $X^*$ implies weak\* convergence
:label: weak-implies-weak-star

Let $X$ be a normed space. If $f_n \rightharpoonup f$ weakly in $X^*$, then $f_n
\xrightarrow{w^*} f$.
```

````{prf:proof}
:class: dropdown

Weak convergence in $X^*$ means $\phi(f_n) \to \phi(f)$ for every $\phi \in
X^{**}$. For any $x \in X$, the canonical image $J(x) \in X^{**}$ acts by
$J(x)(g) = g(x)$. In particular,

$$f_n(x) = J(x)(f_n) \to J(x)(f) = f(x).$$

Since $J(X) \subseteq X^{**}$, weak convergence tests against a larger set of
functionals than weak\* convergence, so the former implies the latter.
````

In summary, we have the chain:

$$\text{strong in } X^* \implies \text{weak in } X^* \implies \text{weak* in } X^*,$$

and neither arrow reverses in general. When $X$ is reflexive ($J$ is surjective),
the last two notions coincide.

```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import matplotlib.pyplot as plt

fig, axes = plt.subplots(1, 3, figsize=(15, 5))
t_line = np.linspace(-2.5, 2.5, 200)

# --- Panel 1: Strong convergence ---
ax = axes[0]

# A foliation (f(u,v) = u + v) in background
for c in np.arange(-3, 4, 0.5):
    alpha = 0.4 if abs(c) < 0.01 else 0.1
    lw = 1.2 if abs(c) < 0.01 else 0.5
    ax.plot(t_line, c - t_line, 'C1', alpha=alpha, lw=lw)

x_target = np.array([1.0, 0.5])
ax.plot(*x_target, 'C3o', ms=12, zorder=10)
ax.text(x_target[0] + 0.12, x_target[1] + 0.12, r'$x$', fontsize=14,
        color='C3', fontweight='bold')

# Points spiraling in
N = 8
for i in range(N):
    r = 1.0 * (1 - i / N)
    ang = 2 * np.pi * i / 5
    pt = x_target + r * np.array([np.cos(ang), np.sin(ang)])
    c_val = i / N
    ax.plot(*pt, 'o', color=plt.cm.viridis(c_val), ms=6, zorder=5)
    if i < N - 1:
        ax.annotate('', xy=x_target, xytext=pt,
                    arrowprops=dict(arrowstyle='->', color=plt.cm.viridis(c_val),
                                    lw=0.8, alpha=0.3))

ax.set_xlim(-0.5, 2.5); ax.set_ylim(-1.0, 2.0)
ax.set_aspect('equal')
ax.set_title('Strong convergence\nPoints cluster, heights converge', fontsize=11)
ax.tick_params(labelsize=8)

# --- Panel 2: Weak convergence ---
ax = axes[1]

# Two different foliations
# f1(u,v) = u (vertical lines)
for c in np.arange(-2, 3, 0.5):
    alpha = 0.35 if abs(c) < 0.01 else 0.1
    lw = 1.2 if abs(c) < 0.01 else 0.5
    ax.axvline(c, color='C1', alpha=alpha, lw=lw)

# f2(u,v) = v (horizontal lines)
for c in np.arange(-2, 3, 0.5):
    alpha = 0.35 if abs(c) < 0.01 else 0.1
    lw = 1.2 if abs(c) < 0.01 else 0.5
    ax.axhline(c, color='C2', alpha=alpha, lw=lw)

# Target
ax.plot(0, 0, 'C3s', ms=10, zorder=10)
ax.text(0.12, -0.2, r'$0$', fontsize=13, color='C3', fontweight='bold')

# Points that stay on the unit circle but whose projections decay
# In R^2 this can't truly happen (weak=strong), so we show a sequence
# whose projections onto both axes shrink (i.e., it does converge strongly too)
# But the CONCEPT is: check each foliation separately
N = 8
angles_seq = np.array([np.pi/4 + 0.6*(-1)**i / (i+1) for i in range(N)])
radii_seq = np.linspace(1.2, 0.15, N)
for i in range(N):
    pt = radii_seq[i] * np.array([np.cos(angles_seq[i]), np.sin(angles_seq[i])])
    c_val = i / N
    ax.plot(*pt, 'o', color=plt.cm.viridis(c_val), ms=6, zorder=5)
    # Draw horizontal and vertical dashed lines to show projections
    ax.plot([pt[0], pt[0]], [0, pt[1]], ':', color='C1', alpha=0.3, lw=0.8)
    ax.plot([0, pt[0]], [pt[1], pt[1]], ':', color='C2', alpha=0.3, lw=0.8)

ax.text(1.7, 1.4, r'$f_1$-heights $\to 0$', fontsize=9, color='C1')
ax.text(-1.8, 1.4, r'$f_2$-heights $\to 0$', fontsize=9, color='C2')

ax.set_xlim(-2.0, 2.2); ax.set_ylim(-1.5, 1.8)
ax.set_aspect('equal')
ax.set_title('Weak convergence\nCheck each foliation separately', fontsize=11)
ax.tick_params(labelsize=8)

# --- Panel 3: Weak* convergence ---
ax = axes[2]

# Fixed points in the space
pts = [(1.2, 0.6, r'$x_1$', 'C3'), (0.3, 1.0, r'$x_2$', 'C2'),
       (-0.5, 0.8, r'$x_3$', 'C4')]
for (px, py, label, color) in pts:
    ax.plot(px, py, 'o', color=color, ms=9, zorder=10)
    ax.text(px + 0.1, py + 0.1, label, fontsize=11, color=color)

# Draw several foliations rotating toward a limit
n_foliations = 5
cmap = plt.cm.plasma
for i in range(n_foliations):
    angle = np.pi / 6 + i * np.pi / (3 * n_foliations)
    a, b = np.cos(angle), np.sin(angle)
    for c in np.arange(-2, 3, 1):
        if abs(b) > 0.01:
            y_line = (c - a * t_line) / b
            mask = (y_line > -2) & (y_line < 2.5)
            ax.plot(t_line[mask], y_line[mask], color=cmap(i / n_foliations),
                    alpha=0.15, lw=0.8)
    if abs(b) > 0.01:
        y_ker = (-a * t_line) / b
        mask = (y_ker > -2) & (y_ker < 2.5)
        ax.plot(t_line[mask], y_ker[mask], color=cmap(i / n_foliations),
                alpha=0.5, lw=1.5)

ax.text(0.3, -1.5, r'$f_1, f_2, f_3, \ldots$ rotate', fontsize=10,
        color='gray', ha='center', style='italic')

ax.set_xlim(-1.5, 2.5); ax.set_ylim(-1.8, 1.8)
ax.set_aspect('equal')
ax.set_title('Weak* convergence\nPoints fixed, foliations rearrange', fontsize=11)
ax.tick_params(labelsize=8)

plt.tight_layout()
plt.show()
```

*The three convergences illustrated schematically. Left (strong): points
physically approach $x$, so their heights in any foliation automatically
converge. Center (weak): we check convergence foliation by foliation. The dashed
lines show projections of each $x_n$ onto two foliations ($f_1$ and $f_2$); weak
convergence asks that these projections converge for every foliation
simultaneously. In $\mathbb{R}^2$ this forces strong convergence too (finitely
many foliations control the norm), but in infinite dimensions points can wander
on a sphere while all foliation heights still converge. Right (weak\*): the
points $x_1, x_2, x_3$ are fixed, and the foliations themselves rotate. Weak\*
convergence asks that the height reading at each fixed point stabilizes as the
foliations change.*


## Convergence of Measures as Weak* Convergence

Measures fit naturally into the foliation picture. By the
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

```{prf:definition} Weak* convergence of measures
:label: weak-star-measures-def

Let $K$ be a compact Hausdorff space and let $(\mu_n)_{n \geq 1}$ be a sequence in $\mathcal{M}(K) = C(K)^*$. We say $\mu_n \xrightarrow{w^*} \mu$ if

$$\int_K g\,d\mu_n \to \int_K g\,d\mu \quad \text{for every } g \in C(K).$$
```

This is much more forgiving than total variation convergence: it only asks that
the measures agree when tested against continuous functions. In the foliation
language: each measure $\mu$ defines a foliation of $C(K)$, and weak\*
convergence means the height readings $\mu(g) = \int g\,d\mu$ stabilize for
every fixed $g$.

```{prf:remark} Connection to probability
:label: weak-star-probability

If $\mu_n$ and $\mu$ are **probability measures** (i.e., $\mu_n \geq 0$, $\mu_n(K) = 1$), then $\int g\,d\mu_n = \mathbb{E}_{\mu_n}[g]$. Weak\* convergence becomes:

$$\mathbb{E}_{\mu_n}[g] \to \mathbb{E}_\mu[g] \quad \text{for every continuous } g \in C(K).$$

This is **convergence in distribution** (also called weak convergence of probability measures in the probability literature). It is the convergence in the central limit theorem: the *distributions* $\mu_n$ of $\frac{1}{\sqrt{n}}\sum_{i=1}^n X_i$ converge to the Gaussian measure $\mu$, meaning the expected value of every continuous test function converges.

Three notions of convergence for probability measures, in increasing strength:

| Convergence | Space / pairing | What converges |
|---|---|---|
| **In distribution** (= weak\* in $C(K)^*$) | Measures $\mu_n \in \mathcal{M}(K) = C(K)^*$ | $\int g\,d\mu_n \to \int g\,d\mu$ for all $g \in C(K)$ |
| **In expectation** (= weak in $L^1$) | Random variables $X_n \in L^1(\Omega)$ | $\mathbb{E}[X_n h] \to \mathbb{E}[Xh]$ for all $h \in L^\infty(\Omega)$ |
| **In total variation** (= strong in $\mathcal{M}(K)$) | Measures $\mu_n \in \mathcal{M}(K)$ | $\|\mu_n - \mu\|_{TV} \to 0$ |

Convergence in distribution lives in $C(K)^*$ and only tests against continuous functions. Convergence in expectation lives in $L^1(\Omega)$ and tests against all bounded measurable functions (it requires the random variables to be defined on a common probability space). Total variation convergence is the norm topology on $\mathcal{M}(K)$.
```


```{prf:example} Converging Dirac masses
:label: dirac-weak-star

The sequence $\delta_{1/n}$ converges weak\* to $\delta_0$ in $C([0,1])^*$. Each $\delta_p$ evaluates a function at the point $p$: $\delta_p(g) = g(p)$. As $p = 1/n$ moves toward $0$, continuity gives $g(1/n) \to g(0)$ for every $g \in C([0,1])$.

In total variation, however, $\|\delta_{1/n} - \delta_0\|_{TV} = 2$ for all $n$, since they assign mass to disjoint points. The measures converge in "statistics" (every continuous observable stabilizes) but remain far apart as objects in $\mathcal{M}([0,1])$.
```


## The Banach-Alaoglu Theorem

**Why should this work?** Each instrument $f \in B_{X^*}$ is determined by its
readings on all objects. And each reading $f(x)$ is just a number trapped in the
interval $[-\|x\|, \|x\|]$. So an instrument is a choice of one bounded number
per object. Now take a sequence of instruments. Focus on a single object $x_1$:
the readings $f_n(x_1)$ are bounded, so Bolzano-Weierstrass gives a convergent
subsequence. Extract a further subsequence to make the readings converge at
$x_2$, then $x_3$, and so on.

This is the same diagonal argument behind Arzelà-Ascoli and compact operators:
whenever there are **countably many** coordinates to control,
Bolzano-Weierstrass plus diagonalization does the job. If $X$ is separable, pick
a countable dense subset $\{x_1, x_2, \ldots\}$, diagonalize to get convergence
on the dense subset, then extend to all of $X$ by density and uniform
boundedness. This gives a complete proof for separable $X$. The full theorem
(non-separable $X$) replaces the diagonal argument with Tychonoff's theorem, but
the core idea is unchanged: each reading is trapped in a bounded interval, and
compactness of intervals forces the readings to settle down.

`````{prf:theorem} Banach-Alaoglu
:label: banach-alaoglu

Let $X$ be a normed space. The closed unit ball $B_{X^*} = \{f \in X^* : \|f\| \leq 1\}$ is compact in the weak\* topology.

````{prf:proof}
:class: dropdown

The idea is to embed $B_{X^*}$ into a product of compact intervals and apply
Tychonoff's theorem.

**Step 1: Embed $B_{X^*}$ into a product space.** Each $f \in B_{X^*}$ is
determined by its values on all $x \in X$. Since $|f(x)| \leq \|f\| \cdot \|x\|
\leq \|x\|$, the value $f(x)$ lies in the interval $I_x = [-\|x\|, \|x\|]$. So
the map

$$\Phi : B_{X^*} \to \prod_{x \in X} I_x, \qquad \Phi(f) = (f(x))_{x \in X}$$

embeds $B_{X^*}$ into the product $P = \prod_{x \in X} I_x$.

**Step 2: The product is compact.** Each $I_x$ is a compact interval in
$\mathbb{R}$. By Tychonoff's theorem, the product $P$ is compact in the product
topology.

**Step 3: $\Phi$ is a homeomorphism onto its image.** The product topology on
$P$ is the topology of pointwise convergence: a net $(g_\alpha)$ converges in
$P$ iff $g_\alpha(x) \to g(x)$ for every $x \in X$. This is exactly the weak\*
topology on $B_{X^*}$. So $\Phi$ is continuous and open onto its image.

**Step 4: The image is closed.** We need to show that $\Phi(B_{X^*})$ is closed
in $P$. Let $(g_\alpha)$ be a net in $\Phi(B_{X^*})$ converging to $g \in P$.
Then $g_\alpha(x) \to g(x)$ for every $x$. Since each $g_\alpha$ is linear:

$$g(\alpha x + \beta y) = \lim g_\alpha(\alpha x + \beta y) = \lim [\alpha g_\alpha(x) + \beta g_\alpha(y)] = \alpha g(x) + \beta g(y),$$

so $g$ is linear. And $|g(x)| = \lim |g_\alpha(x)| \leq \|x\|$, so $\|g\| \leq
1$. Therefore $g \in B_{X^*}$.

Since $\Phi(B_{X^*})$ is a closed subset of the compact space $P$, it is
compact. Since $\Phi$ is a homeomorphism onto its image, $B_{X^*}$ is compact in
the weak\* topology.
````
`````

```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import matplotlib.pyplot as plt
from matplotlib.patches import Polygon

np.random.seed(42)

fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 5.5))

# --- Generate a wild sequence on the l^1 unit sphere ---
N = 30
angles = np.cumsum(np.random.uniform(0.4, 1.8, N))
pts = []
for ang in angles:
    a, b = np.cos(ang), np.sin(ang)
    norm_l1 = abs(a) + abs(b)
    pts.append((a / norm_l1, b / norm_l1))
pts = np.array(pts)

# Limit point on the l^1 sphere
limit = np.array([0.6, 0.4])
lim_normalized = limit / (abs(limit[0]) + abs(limit[1]))

# Build a subsequence that converges toward the limit
subseq_idx = [2, 6, 11, 16, 21, 26, 29]
subseq_pts = []
for j, i in enumerate(subseq_idx):
    t = (j + 1) / (len(subseq_idx) + 1)
    blended = (1 - t**0.7) * pts[i] + t**0.7 * lim_normalized
    blended = blended / (abs(blended[0]) + abs(blended[1]))
    subseq_pts.append(blended)
subseq_pts = np.array(subseq_pts)

# --- Draw unit ball on both panels ---
diamond = np.array([[1, 0], [0, 1], [-1, 0], [0, -1]])
for ax in [ax1, ax2]:
    dm = Polygon(diamond, fill=True, facecolor='C0', alpha=0.08,
                 edgecolor='C0', lw=2)
    ax.add_patch(dm)

# --- Left panel: full sequence bouncing around ---
ax1.plot(pts[:, 0], pts[:, 1], '-', color='gray', alpha=0.25, lw=0.8, zorder=2)
for i in range(N):
    alpha = 0.15 + 0.4 * (i / N)
    ax1.plot(pts[i, 0], pts[i, 1], 'o', color='gray', ms=3, alpha=alpha, zorder=3)

# Highlight subsequence on left panel
for j in range(len(subseq_pts)):
    alpha = 0.4 + 0.6 * (j / len(subseq_pts))
    ax1.plot(subseq_pts[j, 0], subseq_pts[j, 1], 'o', color='C3',
             ms=7, alpha=alpha, zorder=6)

# Limit point
ax1.plot(*lim_normalized, '*', color='C3', ms=16, zorder=10,
         markeredgecolor='white', markeredgewidth=0.8)
ax1.annotate(r'$f^*$', xy=lim_normalized,
             xytext=(lim_normalized[0] + 0.12, lim_normalized[1] + 0.15),
             fontsize=12, color='C3', fontweight='bold')

ax1.set_title('Full sequence (gray) with\nsubsequence (red) highlighted', fontsize=11)
ax1.set_xlim(-1.35, 1.35)
ax1.set_ylim(-1.35, 1.35)
ax1.set_aspect('equal')
ax1.set_xlabel(r'$a$', fontsize=11)
ax1.set_ylabel(r'$b$', fontsize=11)

# --- Right panel: subsequence converging with arrows ---
# Arrows between consecutive subsequence points
for j in range(len(subseq_pts) - 1):
    alpha = 0.25 + 0.55 * (j / len(subseq_pts))
    ax2.annotate('', xy=subseq_pts[j+1], xytext=subseq_pts[j],
                 arrowprops=dict(arrowstyle='->', color='C3', lw=1.5,
                                 alpha=alpha))

# Subsequence points with growing size
for j in range(len(subseq_pts)):
    alpha = 0.4 + 0.6 * (j / len(subseq_pts))
    ms = 5 + 5 * (j / len(subseq_pts))
    ax2.plot(subseq_pts[j, 0], subseq_pts[j, 1], 'o', color='C3',
             ms=ms, alpha=alpha, zorder=6)
    # Label first two and last
    if j == 0:
        ax2.annotate(r'$f_{n_1}$', xy=subseq_pts[j],
                     xytext=(subseq_pts[j, 0] - 0.25, subseq_pts[j, 1] - 0.12),
                     fontsize=10, color='C3')
    elif j == 1:
        ax2.annotate(r'$f_{n_2}$', xy=subseq_pts[j],
                     xytext=(subseq_pts[j, 0] + 0.1, subseq_pts[j, 1] - 0.15),
                     fontsize=10, color='C3')
    elif j == len(subseq_pts) - 1:
        ax2.annotate(r'$f_{n_k}$', xy=subseq_pts[j],
                     xytext=(subseq_pts[j, 0] + 0.1, subseq_pts[j, 1] + 0.1),
                     fontsize=10, color='C3')

# Shrinking circles around limit
for r in [0.45, 0.28, 0.13]:
    circle = plt.Circle(lim_normalized, r, fill=False, edgecolor='C3',
                        ls='--', lw=0.8, alpha=0.2)
    ax2.add_patch(circle)

# Limit point
ax2.plot(*lim_normalized, '*', color='C3', ms=18, zorder=10,
         markeredgecolor='white', markeredgewidth=0.8)
ax2.annotate(r'$f^*$ (limit)', xy=lim_normalized,
             xytext=(lim_normalized[0] - 0.45, lim_normalized[1] + 0.2),
             fontsize=11, color='C3', fontweight='bold',
             arrowprops=dict(arrowstyle='->', color='C3', lw=1, alpha=0.5))

ax2.set_title('Subsequence converging\nto the limit $f^*$', fontsize=11)
ax2.set_xlim(-1.35, 1.35)
ax2.set_ylim(-1.35, 1.35)
ax2.set_aspect('equal')
ax2.set_xlabel(r'$a$', fontsize=11)
ax2.set_ylabel(r'$b$', fontsize=11)

plt.suptitle(r'Banach-Alaoglu: every sequence in $B_{X^*}$ has a weak* convergent subsequence',
             fontsize=12, y=1.02)
plt.tight_layout()
plt.show()
```

*Left: a sequence of instruments $f_n$ (gray) bouncing around the dual unit ball
$B_{X^*}$ (here the $\ell^1$ ball). Each point represents an instrument, i.e., a
foliation of the space -- the point tells you which family of parallel
hyperplanes. The red dots mark a subsequence. Right: the subsequence converges
to the limit instrument $f^*$ (star), with arrows and shrinking circles showing
the approach. Banach-Alaoglu guarantees that such a convergent subsequence
always exists, no matter how wildly the original sequence bounces.*


`````{prf:corollary} Weak compactness in reflexive spaces
:label: reflexive-weak-compactness

Let $X$ be a **reflexive** Banach space. Then every bounded sequence in $X$ has a weakly convergent subsequence. Equivalently, the closed unit ball $B_X$ is compact in the weak topology.

````{prf:proof}
:class: dropdown

Since $X$ is reflexive, the canonical embedding $J : X \to X^{**}$ is
surjective, so $J(B_X) = B_{X^{**}}$. Now apply Banach-Alaoglu to the space
$X^*$: the unit ball $B_{(X^*)^*} = B_{X^{**}}$ is compact in the weak\*
topology of $X^{**}$ (i.e., the topology of pointwise convergence on $X^*$). But
under the identification $J : X \cong X^{**}$, the weak\* topology on $X^{**}$
corresponds exactly to the weak topology on $X$ (both test against elements of
$X^*$). Therefore $B_X$ is weakly compact.

For sequences: given $(x_n)$ with $\|x_n\| \leq C$, the rescaled sequence $(x_n
/ C)$ lies in $B_X$, which is weakly compact. By the Eberlein-Šmulian theorem,
weak compactness and weak sequential compactness coincide in Banach spaces, so
$B_X$ is weakly sequentially compact and there is a weakly convergent
subsequence.
````
`````

This corollary is the reason reflexivity matters in applications. In a reflexive
space, bounded sequences always have weakly convergent subsequences without
leaving the original space $X$. In a non-reflexive space, Banach-Alaoglu only
gives weak\* convergent subsequences in the bidual $X^{**}$, and the limit may
not live in $X$.

### The direct method: a first look

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
