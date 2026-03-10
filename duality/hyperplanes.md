---
kernelspec:
  name: python3
  display_name: Python 3
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/hyperplanes.pdf
    id: duality-hyperplanes-pdf
downloads:
  - id: duality-hyperplanes-pdf
    title: Download PDF
---

# The Geometry of Linear Functionals

Before proving Hahn–Banach, it helps to understand what a linear functional
*looks like* geometrically. This perspective clarifies what duality is really
doing.

## Kernels and level sets

For a nonzero linear functional $f \in X'$ (where $X'$ denotes the algebraic
dual), define two canonical sets:

- $K(f) = \ker(f) = f^{-1}(0) = \{x \in X : f(x) = 0\}$ — the **kernel**
- $I(f) = f^{-1}(1) = \{x \in X : f(x) = 1\}$ — the **unit level set**

Both are level sets of $f$: $K(f)$ is where $f$ vanishes, and $I(f)$ is where
$f$ equals $1$.

Note that $0 \in K(f)$ always (since $f(0) = 0$ by linearity), while $0 \notin
I(f)$ (since $f(0) = 0 \neq 1$). So the kernel passes through the origin; the
unit level set does not.


## The fundamental decomposition

````{prf:proposition} Codimension-1 decomposition
:label: codim-1-decomposition

Let $f \in X'$ be a nonzero linear functional, and let $x_0 \in X$ with $f(x_0) \neq 0$. Then:

1. $K(f)$ is a subspace of **codimension 1** (see {prf:ref}`kernel-codim-1`) — it is "missing exactly one dimension."
2. Every vector $x \in X$ has a **unique** representation
   $$x = y + \lambda x_0, \qquad y \in K(f), \quad \lambda \in \mathbb{R}$$
3. The scalar $\lambda$ is determined: $\lambda = \dfrac{f(x)}{f(x_0)}$.

```{prf:proof}
:class: dropdown

Given any $x \in X$, set $\lambda = f(x)/f(x_0)$ and $y = x - \lambda x_0$. Then
$f(y) = f(x) - \lambda f(x_0) = f(x) - \frac{f(x)}{f(x_0)} f(x_0) = 0$, so $y
\in K(f)$ and $x = y + \lambda x_0$ by construction.

**Uniqueness:** If $x = y_1 + \lambda_1 x_0 = y_2 + \lambda_2 x_0$ with $y_1,
y_2 \in K(f)$, then $(\lambda_1 - \lambda_2)x_0 = y_2 - y_1 \in K(f)$, so
$(\lambda_1 - \lambda_2)f(x_0) = 0$. Since $f(x_0) \neq 0$, we get $\lambda_1 =
\lambda_2$, hence $y_1 = y_2$.

**Codimension 1:** The decomposition gives $X = K(f) \oplus \text{span}(x_0)$.
Since $\text{span}(x_0)$ is one-dimensional, $K(f)$ has codimension 1 — it is a
maximal proper subspace, i.e., a **hyperplane through the origin**.
```
````


## The foliation picture

The decomposition tells us exactly how $f$ organizes the space geometrically.

Every $x \in X$ is uniquely $x = y + \lambda x_0$ with $y \in K(f)$, and $f(x) =
\lambda f(x_0)$. So the level sets of $f$ are:

$$f^{-1}(c) = \left\{y + \frac{c}{f(x_0)}\,x_0 : y \in K(f)\right\} = K(f) + \frac{c}{f(x_0)}\,x_0$$

These are parallel copies of $K(f)$, shifted along the $x_0$-direction. They
**foliate** $X$ — every point lies on exactly one level set — and $f$ assigns a
"height" $c$ to each slice.

If we normalize so that $f(x_0) = 1$:

- $K(f) = f^{-1}(0)$ is the slice through the origin.
- $I(f) = f^{-1}(1) = K(f) + x_0$ is the slice one step along $x_0$.
- $f^{-1}(n) = K(f) + n\,x_0$ for any integer $n$ — evenly spaced slices.

```{prf:example} Foliation in $\mathbb{R}^3$
Take $f(x,y,z) = 2x + 3y - z$.

- $K(f) = \{2x + 3y - z = 0\}$ — a plane through the origin.
- Pick $x_0 = (1, 0, 2)$; then $f(x_0) = 2$.
- The level sets $f^{-1}(c) = \{2x + 3y - z = c\}$ are parallel planes.
- Moving along $x_0$ increases $f$ by 2 per unit step.
```

```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import matplotlib.pyplot as plt

# Color map for the five highlighted level sets c = -2, -1, 0, 1, 2
level_colors = {-2: 'C4', -1: 'C3', 0: 'C0', 1: 'C1', 2: 'C2'}

fig, axes = plt.subplots(1, 2, figsize=(14, 6))
t = np.linspace(-3, 3, 100)

# Left: foliation by f(x,y) = x + y in R^2
ax = axes[0]
for c in np.arange(-5, 5, 0.5):
    y_line = c - t
    if c in level_colors:
        ax.plot(t, y_line, color=level_colors[c], alpha=0.9, lw=2.5)
    else:
        ax.plot(t, y_line, color='gray', alpha=0.2, lw=0.7)

ax.set_xlim(-2.5, 2.5)
ax.set_ylim(-2.5, 2.5)
ax.set_aspect('equal')
ax.axhline(0, color='k', lw=0.5, alpha=0.3)
ax.axvline(0, color='k', lw=0.5, alpha=0.3)
ax.set_title(r'Foliation by $f(x,y) = x + y$', fontsize=14)
ax.set_xlabel(r'$x$', fontsize=12)
ax.set_ylabel(r'$y$', fontsize=12)
ax.tick_params(labelsize=11)
for c, col in level_colors.items():
    ax.plot([], [], color=col, lw=2.5, label=f'$c = {c}$')
ax.legend(fontsize=11, loc='upper right', ncol=1)

# Right: foliation by g(x,y) = 2(x + y) — same kernel, denser spacing
ax = axes[1]
for c in np.arange(-9, 9, 1):
    y_line = c / 2 - t  # g = 2(x+y) = c  =>  x+y = c/2
    if c in level_colors:
        ax.plot(t, y_line, color=level_colors[c], alpha=0.9, lw=2.5)
    else:
        ax.plot(t, y_line, color='gray', alpha=0.2, lw=0.7)

ax.set_xlim(-2.5, 2.5)
ax.set_ylim(-2.5, 2.5)
ax.set_aspect('equal')
ax.axhline(0, color='k', lw=0.5, alpha=0.3)
ax.axvline(0, color='k', lw=0.5, alpha=0.3)
ax.set_title(r'Foliation by $g(x,y) = 2(x + y)$: denser spacing', fontsize=14)
ax.set_xlabel(r'$x$', fontsize=12)
ax.set_ylabel(r'$y$', fontsize=12)
ax.tick_params(labelsize=11)
for c, col in level_colors.items():
    ax.plot([], [], color=col, lw=2.5, label=f'$c = {c}$')
ax.legend(fontsize=11, loc='upper right', ncol=1)

plt.tight_layout()
plt.show()
```

*Level sets of $f(x,y) = x + y$ (left) and $g(x,y) = 2(x+y)$ (right). Both
functionals share the same kernel $K(f) = K(g) = \{x + y = 0\}$, but $g$ has
twice the spacing density: the $c = 1$ level set of $g$ sits where the $c = 1/2$
level set of $f$ would be.*

### What the kernel and scale each determine

A nonzero functional is determined by two independent pieces of geometric data:

**1. The kernel determines the orientation of the slices.** Two functionals with
the same kernel produce exactly the same family of parallel hyperplanes. The
kernel tells you *which directions are horizontal* (directions lying in $K(f)$)
and *which direction is transverse*.

**2. The scale determines the spacing between slices.** If $g = 2f$, then
$\ker(g) = \ker(f)$ — same orientation, same family of parallel hyperplanes. But
$g^{-1}(1) = f^{-1}(1/2)$, which sits halfway between $f^{-1}(0)$ and
$f^{-1}(1)$. Rescaling $f$ by $\lambda$ doesn't rotate the slices — it
compresses or stretches the spacing between them.

## Functionals are determined by their kernels

The decomposition immediately yields a powerful uniqueness result.

````{prf:proposition}
:label: kernel-determines-functional

If $f, g : X \to \mathbb{R}$ are nonzero linear functionals with $\ker(f) = \ker(g)$, then $f = \lambda g$ for some scalar $\lambda \neq 0$.

```{prf:proof}
:class: dropdown

Pick any $x_0 \notin \ker(f) = \ker(g)$. By the decomposition, every $x \in X$
can be written as $x = y + \frac{f(x)}{f(x_0)}\,x_0$ with $y \in \ker(f) =
\ker(g)$. Applying $g$:

$$g(x) = g(y) + \frac{f(x)}{f(x_0)}\,g(x_0) = 0 + \frac{g(x_0)}{f(x_0)}\,f(x)$$

since $g(y) = 0$ (because $y \in \ker(g)$). Setting $\lambda = g(x_0)/f(x_0)$
gives $g = \lambda f$.
```
````

**Consequence for the dual space:** Classifying linear functionals up to scaling
is the same as classifying codimension-1 subspaces. The projective algebraic
dual $X'/\!\sim$ (where $f \sim \lambda f$ for $\lambda \neq 0$) is in bijection
with the set of hyperplanes through the origin.


## Characterizing continuity via hyperplanes

Here is where the algebraic vs. topological dual distinction becomes geometric.
The key fact is surprisingly sharp: **a hyperplane is either closed (and nowhere
dense) or dense in $X$ — there is nothing in between.**

````{prf:lemma}
:label: closed-subspace-empty-interior

A proper closed subspace of a normed space has empty interior (hence is nowhere dense).

```{prf:proof}
:class: dropdown

Let $M \subsetneq X$ be a proper closed subspace. Suppose for contradiction that
$M$ contains an open ball $B(x, r)$ for some $x \in M$, $r > 0$. Since $M$ is a
subspace and $x \in M$, for any $v \in B(0, r)$ we have $v = (x + v) - x$, and
$x + v \in B(x, r) \subset M$, so $v \in M$. Thus $B(0, r) \subset M$. But then
for any $y \in X$ with $y \neq 0$, the vector $\frac{r}{2\|y\|}\,y$ lies in
$B(0, r) \subset M$, so $y \in M$ (since $M$ is a subspace). This gives $M = X$,
contradicting properness.
```
````

:::{admonition} Why "empty interior" sounds wrong at first
:class: warning

Interior here means in the **full topology of $X$**, not the relative topology
on $M$. The $x$-axis in $\mathbb{R}^2$ looks solid from the inside, but any open
ball in $\mathbb{R}^2$ escapes into the $y$-direction — the subspace is
"infinitely thin" when viewed from the ambient space.
:::

So: **a continuous linear functional has a closed kernel, and this kernel is a
"thin" hyperplane** — a codimension-1 subspace with empty interior in $X$.

````{prf:lemma}
:label: codim-1-closed-or-dense

A codimension-1 subspace of a normed space is either closed or dense.

```{prf:proof}
:class: dropdown

Let $K(f)$ be a codimension-1 subspace (the kernel of some nonzero $f$). Its
closure $\overline{K(f)}$ is a closed subspace containing $K(f)$. Since $K(f)$
has codimension 1, there are only two possibilities:

- $\overline{K(f)} = K(f)$ — in which case $K(f)$ is closed.
- $\overline{K(f)} \supsetneq K(f)$ — but then $\overline{K(f)}$ is a closed
  subspace strictly containing a codimension-1 subspace, so it must be all of
  $X$. Hence $K(f)$ is dense in $X$.

There is no intermediate option.
```
````

````{prf:proposition} Continuity via the kernel
:label: continuity-via-kernel

A nonzero linear functional $f : X \to \mathbb{R}$ is continuous if and only if $\ker(f)$ is closed.

```{prf:proof}
:class: dropdown

**($\Rightarrow$):** If $f$ is continuous, then $\ker(f) = f^{-1}(\{0\})$ is the
preimage of a closed set, hence closed.

**($\Leftarrow$):** Suppose $\ker(f)$ is closed and $f \neq 0$. Pick $x_0$ with
$f(x_0) \neq 0$; by the decomposition, $X = \ker(f) \oplus \text{span}(x_0)$.
Since $\ker(f)$ is closed, $x_0$ has positive distance from $\ker(f)$: set
$\delta = \text{dist}(x_0, \ker(f)) > 0$. For any $x = y + \lambda x_0$ with $y
\in \ker(f)$:

$$\|x\| = \|y + \lambda x_0\| \geq |\lambda| \cdot \text{dist}(x_0, \ker(f)) = |\lambda|\delta$$

(since $-y/\lambda \in \ker(f)$ when $\lambda \neq 0$, so $\|x_0 + y/\lambda\|
\geq \delta$, and multiplying by $|\lambda|$ gives $\|x\| \geq
|\lambda|\delta$). Therefore:

$$|f(x)| = |\lambda| \cdot |f(x_0)| \leq \frac{|f(x_0)|}{\delta}\,\|x\|$$

So $f$ is bounded with $\|f\| \leq |f(x_0)|/\delta$.
```
````

```{prf:remark} Connection to the quotient norm
:class: dropdown

The quantity $\delta = \operatorname{dist}(x_0, \ker(f))$ appearing in the proof
above is the quotient norm $\|[x_0]\|_{X/\ker(f)}$ (see
{prf:ref}`quotient-norm`). The closedness of $\ker(f)$ is essential: it
guarantees that the quotient norm is a genuine norm, so that $\|[x_0]\| > 0$ for
$x_0 \notin \ker(f)$.

In fact, the entire proof is the quotient perspective in disguise. The functional
$f$ factors through the quotient as

$$X \xrightarrow{\;\pi\;} X/\ker(f) \xrightarrow{\;\widetilde{f}\;} \mathbb{R}$$

where $\pi$ is the canonical projection and $\widetilde{f}$ is the isomorphism
from the {prf:ref}`first-isomorphism-theorem`. Since $X/\ker(f)$ is
one-dimensional, $\widetilde{f}$ is automatically bounded (all norms on
$\mathbb{R}$ are equivalent), and $\pi$ is bounded with $\|\pi\| \leq 1$. The
composite $f = \widetilde{f} \circ \pi$ is therefore bounded.
```

Combining everything:

- $f \in X^*$ (continuous) $\iff$ $K(f)$ is **closed** $\implies$ $K(f)$ is
  **nowhere dense**: a thin, clean hyperplane with empty interior. The space is
  sliced into well-separated parallel copies of $K(f)$, and the height function
  varies continuously.

- $f \in V' \setminus X^*$ (discontinuous) $\iff$ $K(f)$ is **not closed**
  $\implies$ $K(f)$ is **dense**: the hyperplane comes arbitrarily close to
  every point in $X$.

There is nothing in between: every hyperplane is either cleanly closed or
pathologically dense.

```{prf:remark} Dense hyperplanes are pathological
:class: dropdown

If $K(f)$ is dense, then *every* level set $f^{-1}(c)$ is also dense. Points at height $0$, height $1$, and height $1{,}000{,}000$ are all interleaved at arbitrarily fine scales throughout the space. With a continuous functional, you'd see clean parallel bands of color, smoothly transitioning. With a discontinuous functional, every color appears in every tiny ball.

Concretely: if $f$ is discontinuous, then for any $\varepsilon > 0$ and any $M > 0$, there exists $x$ with $\|x\| < \varepsilon$ but $|f(x)| > M$. The slicing exists algebraically, but the height function is wildly discontinuous. This is why continuous functionals — the ones with closed, nowhere-dense kernels — are the only ones useful for analysis.
```


## A Worked Example: Hahn–Banach Extension in $\mathbb{R}^2$

The Hahn–Banach theorem, stated in the hyperplane language, says: **if you know
the heights of points along a subspace, you can extend the height function to
the entire space by choosing a closed hyperplane.**

We make this explicit with a worked example. We use $\mathbb{R}^2$ with the
$\ell^\infty$ norm $\|(x,y)\|_\infty = \max(|x|, |y|)$, so the unit ball is a
**square**.

:::{admonition} Why the $\ell^\infty$ norm and not Euclidean?
:class: note

With the Euclidean norm (round unit ball), the Hahn–Banach extension turns out
to be **unique** — the roundness of the ball forces a single choice. This is a
general fact about Hilbert spaces: the Riesz representation theorem pins down
the unique extension.

With the $\ell^\infty$ norm (square unit ball), the extension is **non-unique**
— there is a whole interval of valid choices, each giving a different kernel.
This is the generic situation in Banach spaces.
:::

**Step 1: Define $f$ on a subspace.**

Let $M = \text{span}((1,1))$. Define $f$ on $M$ by $f(t(1,1)) = t$. Check the
norm: $|f(t(1,1))| = |t|$ and $\|t(1,1)\|_\infty = |t| \cdot \|(1,1)\|_\infty =
|t|$. So $\|f\| = 1$ on $M$.

We know the heights along the diagonal line $M$: the origin has height 0, the
point $(1/2, 1/2)$ has height $1/2$, the point $(1,1)$ has height 1.

**Step 2: Decompose.**

Pick $z = (1,-1) \notin M$ as the new direction. Every $(x,y) \in \mathbb{R}^2$
decomposes as:

$$(x,y) = \underbrace{\frac{x+y}{2}(1,1)}_{\text{component in }M} + \underbrace{\frac{x-y}{2}}_{\text{coefficient }\alpha}\,(1,-1)$$

**Step 3: The extension is determined by one number.**

Set $c = F(z) = F(1,-1)$ — the height we assign to the new direction. By
linearity:

$$F(x,y) = \frac{x+y}{2} + \frac{x-y}{2} \cdot c = \frac{1+c}{2}\,x + \frac{1-c}{2}\,y$$

Note $a + b = 1$ where $a = (1+c)/2$ and $b = (1-c)/2$, ensuring $F(1,1) = 1 =
f(1,1)$.

**Step 4: Find which values of $c$ are valid.**

We need $\|F\|_{\text{op}} \leq 1$ in the $\ell^\infty$ norm. For a linear
functional $F(x,y) = ax + by$ on $(\mathbb{R}^2, \|\cdot\|_\infty)$, the
operator norm is $\|F\| = |a| + |b|$. The constraint $|a| + |b| \leq 1$ combined
with $a + b = 1$ forces $a, b \geq 0$, giving:

$$\boxed{c \in [-1, 1]}$$

Every $c$ in this interval gives a valid norm-preserving extension. The
constraint $|a| + |b| \leq 1$ is the $\ell^1$ unit ball in the $(a,b)$-plane,
and $a + b = 1$ is a line cutting through it. The valid extensions correspond to
the segment where the line meets the ball.

```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import matplotlib.pyplot as plt
from matplotlib.patches import Polygon

fig, ax = plt.subplots(1, 1, figsize=(6, 5))

# The l^1 unit ball: |a| + |b| <= 1
diamond = np.array([[1, 0], [0, 1], [-1, 0], [0, -1], [1, 0]])
dm = Polygon(diamond[:-1], fill=True, facecolor='C0', alpha=0.15,
             edgecolor='C0', lw=2, label=r'$|a| + |b| \leq 1$')
ax.add_patch(dm)

# The line a + b = 1
t = np.linspace(-0.5, 1.5, 200)
ax.plot(t, 1 - t, 'C3', lw=2, label=r'$a + b = 1$')

# The feasible segment: a + b = 1 and |a| + |b| <= 1 => a, b >= 0
# So a in [0, 1], b = 1 - a in [0, 1]
a_seg = np.linspace(0, 1, 100)
b_seg = 1 - a_seg
ax.plot(a_seg, b_seg, 'C1', lw=4, alpha=0.8, solid_capstyle='round',
        label=r'Valid extensions')

# Mark the three special cases
cases = [(1, 0, r'$c=1$: $F=x$'), (0.5, 0.5, r'$c=0$: $F=\frac{x+y}{2}$'),
         (0, 1, r'$c=-1$: $F=y$')]
for (a_pt, b_pt, label) in cases:
    ax.plot(a_pt, b_pt, 'ko', ms=7, zorder=10)
    ax.text(a_pt + 0.05, b_pt + 0.06, label, fontsize=9)

ax.set_xlim(-1.3, 1.5)
ax.set_ylim(-1.3, 1.5)
ax.set_aspect('equal')
ax.axhline(0, color='k', lw=0.5, alpha=0.3)
ax.axvline(0, color='k', lw=0.5, alpha=0.3)
ax.set_xlabel(r'$a$')
ax.set_ylabel(r'$b$')
ax.set_title(r'Feasible $(a,b)$: line $a+b=1$ meets $\ell^1$ ball', fontsize=12)
ax.legend(fontsize=9, loc='lower left')
plt.tight_layout()
plt.show()
```

*The $\ell^1$ unit ball $|a| + |b| \leq 1$ (diamond) is the dual ball of
$(\mathbb{R}^2, \|\cdot\|_\infty)$, so the operator norm constraint $\|F\| \leq
1$ requires $(a,b)$ to lie inside it. The extension constraint $a + b = 1$
(ensuring $F = f$ on $M$) is a line. Valid extensions are the segment where the
line meets the diamond — parametrized by $c \in [-1, 1]$.*

**Step 5: Each $c$ gives a different kernel.**

- $c = 0$: $F(x,y) = \frac{x+y}{2}$. Kernel: $x + y = 0$ (the anti-diagonal).
- $c = 1$: $F(x,y) = x$. Kernel: $x = 0$ (the $y$-axis).
- $c = -1$: $F(x,y) = y$. Kernel: $y = 0$ (the $x$-axis).

```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import matplotlib.pyplot as plt
from matplotlib.patches import Polygon

fig, axes = plt.subplots(1, 3, figsize=(16, 6))

# The l-infinity unit ball (square)
square = np.array([[-1, -1], [1, -1], [1, 1], [-1, 1], [-1, -1]])

# The subspace M = span((1,1))
t_M = np.linspace(-2, 2, 100)

cases = [
    (0, r'$c = 0$: $F = \frac{x+y}{2}$', r'Kernel: $x+y=0$'),
    (1, r'$c = 1$: $F = x$', r'Kernel: $x=0$'),
    (-1, r'$c = -1$: $F = y$', r'Kernel: $y=0$'),
]

for ax, (c_val, title, ker_label) in zip(axes, cases):
    a = (1 + c_val) / 2
    b = (1 - c_val) / 2

    # Draw the unit square
    sq_patch = Polygon(square[:-1], fill=True, facecolor='C0', alpha=0.15, edgecolor='C0', lw=2.5)
    ax.add_patch(sq_patch)

    # Draw level sets of F(x,y) = ax + by = const
    for level in np.arange(-2.5, 3.0, 0.5):
        t = np.linspace(-2.5, 2.5, 200)
        if abs(b) > 1e-10:
            y_line = (level - a * t) / b
            mask = (y_line > -2.5) & (y_line < 2.5)
            lw = 2.5 if abs(level - round(level)) < 0.01 and level == int(level) else 0.8
            alpha = 0.8 if lw > 1 else 0.3
            color = 'C3' if abs(level) < 0.01 else ('C1' if abs(level - 1) < 0.01 else 'gray')
            ax.plot(t[mask], y_line[mask], color=color, alpha=alpha, lw=lw)
        else:
            if abs(a) > 1e-10:
                x_val = level / a
                if -2.5 < x_val < 2.5:
                    lw = 2.5 if abs(level - round(level)) < 0.01 and level == int(level) else 0.8
                    alpha = 0.8 if lw > 1 else 0.3
                    color = 'C3' if abs(level) < 0.01 else ('C1' if abs(level - 1) < 0.01 else 'gray')
                    ax.axvline(x_val, color=color, alpha=alpha, lw=lw)

    # Draw the subspace M
    ax.plot(t_M, t_M, 'k--', alpha=0.4, lw=1.5, label=r'$M = \mathrm{span}(1,1)$')

    # Mark special points
    ax.plot(1, 1, 'ko', ms=7, zorder=5)
    ax.text(1.1, 1.1, r'$(1,1)$', fontsize=12)
    ax.plot(0.5, 0.5, 'ko', ms=5, zorder=5)
    ax.plot(0, 0, 'ko', ms=5, zorder=5)

    ax.set_xlim(-2.6, 2.6)
    ax.set_ylim(-2.6, 2.6)
    ax.set_aspect('equal')
    ax.set_title(f'{title}\n{ker_label}', fontsize=13)
    ax.set_xlabel(r'$x$', fontsize=12)
    ax.set_ylabel(r'$y$', fontsize=12)
    ax.tick_params(labelsize=11)

    # Color legend
    ax.plot([], [], 'C3', lw=2.5, label=r'$F = 0$ (kernel)')
    ax.plot([], [], 'C1', lw=2.5, label=r'$F = 1$')
    ax.plot([], [], 'gray', lw=1, label='Other levels')
    ax.legend(fontsize=10, loc='upper right')

plt.tight_layout()
plt.show()
```

*Three norm-preserving extensions of $f$ from $M = \mathrm{span}(1,1)$ to all of
$\mathbb{R}^2$, corresponding to $c = 0, 1, -1$. In each panel, the
$\ell^\infty$ unit square (shaded) fits between the $F = -1$ and $F = 1$ level
sets, confirming $\|F\| = 1$. The kernel (red) and the subspace $M$ (dashed)
differ in each case, but $F(1,1) = 1$ in all three.*

:::{tip} Takeaway
Same functional on $M$. Three different extensions. Three different kernels. In
each case the unit square fits between the level sets $F^{-1}(-1)$ and
$F^{-1}(1)$ — the norm constraint $\|F\| \leq 1$ is satisfied because the flat
sides of the square allow the kernel to tilt freely. With a round ball, only one
tilt would work. **Hahn–Banach says: in any Banach space, no matter how large,
at least one valid $c$ always exists.**
:::


### Visualizing the full family of extensions

Every $c \in [-1, 1]$ gives a different valid extension. Each extension defines
a **strip** between $F^{-1}(-1)$ and $F^{-1}(1)$, and the norm constraint $\|F\|
= 1$ means the unit square must fit inside that strip. The unit ball is the
intersection of all such strips.

```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import matplotlib.pyplot as plt
from matplotlib.patches import Polygon

fig, ax = plt.subplots(1, 1, figsize=(8, 8))

square = np.array([[-1, -1], [1, -1], [1, 1], [-1, 1], [-1, -1]])
sq_patch = Polygon(square[:-1], fill=True, facecolor='C0', alpha=0.15, edgecolor='C0', lw=2.5,
                   zorder=5)
ax.add_patch(sq_patch)

# Draw F^{-1}(1) and F^{-1}(-1) for various c values
# F(x,y) = ax + by with a = (1+c)/2, b = (1-c)/2
# F = ±1  =>  ax + by = ±1
c_values = np.linspace(-1, 1, 9)
cmap = plt.cm.coolwarm

t = np.linspace(-3.5, 3.5, 300)
for i, c_val in enumerate(c_values):
    a = (1 + c_val) / 2
    b = (1 - c_val) / 2
    color = cmap(i / (len(c_values) - 1))

    for level in [1, -1]:
        if abs(b) > 1e-10:
            y_line = (level - a * t) / b
            mask = (y_line > -3.5) & (y_line < 3.5)
            ax.plot(t[mask], y_line[mask], color=color, alpha=0.6, lw=1.8)
        else:
            # b = 0, a = 1: x = ±1
            ax.axvline(level, color=color, alpha=0.6, lw=1.8)

    # Lightly shade the strip for a few representative values
    if abs(c_val) < 0.01 or abs(abs(c_val) - 1) < 0.01:
        if abs(b) > 1e-10:
            y_upper = (1 - a * t) / b
            y_lower = (-1 - a * t) / b
            ax.fill_between(t, y_lower, y_upper, alpha=0.04, color=color)

# Mark (1,1) — all F^{-1}(1) lines pass through it
ax.plot(1, 1, 'ko', ms=8, zorder=10)
ax.text(1.12, 1.12, r'$(1,1)$', fontsize=13)

# Mark (-1,-1) — all F^{-1}(-1) lines pass through it
ax.plot(-1, -1, 'ko', ms=8, zorder=10)
ax.text(-1.35, -1.2, r'$(-1,-1)$', fontsize=13)

# Draw the subspace M
ax.plot(t, t, 'k--', alpha=0.3, lw=1.5, label=r'$M$', zorder=1)

ax.set_xlim(-2.8, 2.8)
ax.set_ylim(-2.8, 2.8)
ax.set_aspect('equal')
ax.set_title(r'Strips $F^{-1}(-1)$ to $F^{-1}(1)$ for all valid extensions', fontsize=14)
ax.set_xlabel(r'$x$', fontsize=12)
ax.set_ylabel(r'$y$', fontsize=12)
ax.tick_params(labelsize=11)

# Colorbar
sm = plt.cm.ScalarMappable(cmap=cmap, norm=plt.Normalize(-1, 1))
sm.set_array([])
cbar = plt.colorbar(sm, ax=ax, shrink=0.7)
cbar.ax.tick_params(labelsize=11)
cbar.set_label(r'$c = F(1,-1)$', fontsize=12)

plt.tight_layout()
plt.show()
```

*Each valid extension $F$ (parametrized by $c \in [-1,1]$) defines a strip
between $F^{-1}(-1)$ and $F^{-1}(1)$, shown as a pair of lines in matching
color. The $\ell^\infty$ unit square (shaded) fits inside every strip. All
$F^{-1}(1)$ lines pass through $(1,1)$ and all $F^{-1}(-1)$ lines pass through
$(-1,-1)$. The unit ball is exactly the intersection of all these strips, which
is the geometric content of the sup formula $\|x\| = \sup_{\|F\| \leq 1}
|F(x)|$.*

