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

# Weak Convergence

:::{tip} Big Idea
Weak convergence tests a sequence against every linear functional: $x_n
\rightharpoonup x$ means $f(x_n) \to f(x)$ for all $f \in X^*$. Each functional
is a "measuring instrument," and weak convergence asks that every instrument
reading stabilizes. This is strictly weaker than norm convergence in infinite
dimensions (objects can keep bouncing while all readings settle), but strong
enough to extract limits in applications. In particular, weakly convergent
sequences are automatically bounded (Banach-Steinhaus), and compact operators
upgrade weak convergence to strong convergence.
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
