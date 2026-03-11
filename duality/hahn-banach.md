---
kernelspec:
  name: python3
  display_name: Python 3
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/hahn-banach.pdf
    id: duality-hahn-banach-pdf
downloads:
  - id: duality-hahn-banach-pdf
    title: Download PDF
---

# The Hahn–Banach Theorem


`````{prf:theorem} Hahn–Banach theorem
:label: hahn-banach

Let $X$ be a normed space and $M \subset X$ a linear subspace. Let $f \in M^*$
with $|f(x)| \leq k\|x\|$ for all $x \in M$. Then there exists an extension $F
\in X^*$ of $f$ to all of $X$ with $|F(x)| \leq k\|x\|$ for all $x \in X$.

**Note** that $F$ is not necessarily unique.

````{prf:proof}
:class: dropdown

The proof has three ingredients. The first two are structural; the third is
where the analysis lives.

**Ingredient 1: Zorn's lemma setup.**

Define the poset:

$$E = \{(g, G) : G \supseteq M \text{ is a subspace}, \; g \text{ extends } f \text{ on } G, \; |g(x)| \leq k\|x\| \;\forall x \in G\}$$

Order by extension: $(h, H) \leq (g, G)$ if $H \subseteq G$ and $g|_H = h$. This
is nonempty ($(f, M) \in E$), chains have upper bounds (take the union), so Zorn
gives a maximal element $(F, W)$.

**Ingredient 2: Maximal implies total.**

Suppose $W \neq X$. Pick $z \in X \setminus W$ and set $Z = W + \text{span}(z)$.
By the {prf:ref}`codimension-1 decomposition <codim-1-decomposition>`, every
element of $Z$ can be written uniquely as $w + \alpha z$ with $w \in W$, $\alpha
\in \mathbb{R}$. We want to define:

$$\tilde{F}(w + \alpha z) = F(w) + \alpha c$$

for some constant $c$. If we can find *any* valid $c$, then $(\tilde{F}, Z)$
strictly extends $(F, W)$, contradicting maximality.

**Ingredient 3: The constant $c$ exists.**

The requirement $|\tilde{F}(w + \alpha z)| \leq k\|w + \alpha z\|$ constrains
$c$ to lie in an interval. The existing bound $|F(\cdot)| \leq k\|\cdot\|$ on
$W$, combined with the **triangle inequality**, guarantees that the lower bound
on $c$ is $\leq$ the upper bound. The interval is nonempty.

Since $c$ exists, we can extend, contradicting maximality. Therefore $W = X$.
````

```{admonition} What to take away
:class: important

- **Ingredients 1 and 2** follow the same Zorn's lemma template as the Hamel
  basis proof, combined with the codimension-1 decomposition. No new ideas are
  needed.
- **Ingredient 3** is the only piece that requires actual work, and the only
  tool it uses is the **triangle inequality**. This is where the assumption that
  we're in a *normed* space matters — and it's exactly the property that fails
  in $L^p$ for $0 < p < 1$, which is why the dual collapses there.
```
`````


## Geometric Consequences

The corollaries of Hahn–Banach are all **separation results** — they say you can
always find a hyperplane that separates things.


````{prf:corollary} The distinguishing property
:label: hb-separation

Let $x, y \in X$. If $f(x) = f(y)$ for all $f \in X^*$ then $x = y$.

```{prf:proof}
:class: dropdown

If $x \neq y$, define $\varphi(\alpha(x - y)) = \alpha\|x - y\|$ on
$\text{span}(x - y)$. Then $\|\varphi\| = 1$ and Hahn–Banach extends $\varphi$
to $F \in X^*$ with $F(x) - F(y) = F(x-y) = \|x-y\| \neq 0$, contradicting the
assumption.
```
````

The contrapositive gives the intuition: if two points are on the *same* level
set for *every possible* foliation, no matter how you orient the hyperplanes,
then they must be the same point.

```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import matplotlib.pyplot as plt
from matplotlib.patches import Polygon

fig, ax = plt.subplots(figsize=(3.6, 3.3))

square_verts = np.array([[-1, -1], [1, -1], [1, 1], [-1, 1]])
sq = Polygon(square_verts, fill=True, facecolor='C0', alpha=0.1, edgecolor='C0', lw=2)
ax.add_patch(sq)

x_pt = np.array([1.5, 0.8])
y_pt = np.array([-0.5, 1.3])
ax.plot(*x_pt, 'C3o', ms=7, zorder=5)
ax.plot(*y_pt, 'C2o', ms=7, zorder=5)
ax.text(x_pt[0]+0.1, x_pt[1]+0.1, r'$x$', fontsize=10, color='C3')
ax.text(y_pt[0]+0.1, y_pt[1]+0.1, r'$y$', fontsize=10, color='C2')

# Foliation by F(u,v) = u
for level in np.arange(-2, 3, 0.5):
    alpha = 0.6 if level == int(level) else 0.2
    lw = 1.2 if level == int(level) else 0.5
    ax.axvline(level, color='gray', alpha=alpha, lw=lw)

# Level sets through x and y
ax.axvline(x_pt[0], color='C3', lw=1.5, alpha=0.6, ls='--', label=rf'$F(x) = {x_pt[0]}$')
ax.axvline(y_pt[0], color='C2', lw=1.5, alpha=0.6, ls='--', label=rf'$F(y) = {y_pt[0]}$')

ax.set_xlim(-2.2, 2.6)
ax.set_ylim(-2.2, 2.2)
ax.set_aspect('equal')
ax.set_title(r'Separation of points: $F(u,v) = u$ gives $F(x) \neq F(y)$', fontsize=9)
ax.set_xlabel(r'$u$', fontsize=9); ax.set_ylabel(r'$v$', fontsize=9)
ax.tick_params(labelsize=8)
ax.legend(fontsize=8, loc='upper right')

plt.tight_layout()
plt.show()
```

*The functional $F(u,v) = u$ assigns different heights to $x$ and $y$. A level
set between these heights is the separating hyperplane. If two points agree on
every foliation, they must be the same point.*


````{prf:corollary} Norming property
:label: hb-norming

For each $x \in X$, there exists $f \in X^*$ with $f(x) = \|x\|$ and $\|f\|_{\text{op}} = 1$.

```{prf:proof}
:class: dropdown

Define $f(\alpha x) = \alpha\|x\|$ on $\text{span}(x)$. Then $|f(\alpha x)| =
|\alpha|\|x\| = \|\alpha x\|$, so $\|f\| = 1$ on $\text{span}(x)$. Hahn–Banach
extends to $F \in X^*$ with $\|F\| = 1$ and $F(x) = \|x\|$.
```
````

```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import matplotlib.pyplot as plt
from matplotlib.patches import Polygon

fig, ax = plt.subplots(figsize=(3.6, 3.3))

square_verts = np.array([[-1, -1], [1, -1], [1, 1], [-1, 1]])
sq = Polygon(square_verts, fill=True, facecolor='C0', alpha=0.1, edgecolor='C0', lw=2)
ax.add_patch(sq)

x0 = np.array([1.8, 0.5])
ax.plot(*x0, 'C3o', ms=7, zorder=5)
ax.text(x0[0]+0.05, x0[1]+0.15, r'$x_0$', fontsize=10, color='C3')
ax.annotate('', xy=x0, xytext=(0, 0),
            arrowprops=dict(arrowstyle='->', color='C3', lw=1.2))

# Foliation by F(u,v) = u; ||x0||_inf = 1.8
for level in np.arange(-2, 3, 0.5):
    alpha = 0.5 if level == int(level) else 0.2
    lw = 1.2 if level == int(level) else 0.5
    color = 'C1' if abs(level - 1) < 0.01 or abs(level + 1) < 0.01 else 'gray'
    ax.axvline(level, color=color, alpha=alpha, lw=lw)

# Strip [-1, 1]
ax.axvspan(-1, 1, alpha=0.08, color='C1')
ax.axvline(x0[0], color='C3', lw=1.5, alpha=0.7, ls='--', label=rf'$F(x_0) = {x0[0]} = \|x_0\|_\infty$')
ax.text(0, -2.0, r'$B_X$ fits in strip $|F| \leq 1$', fontsize=8, ha='center', color='C1')

ax.set_xlim(-2.6, 2.6)
ax.set_ylim(-2.6, 2.6)
ax.set_aspect('equal')
ax.set_title(r'Norm-attaining functional: $F(x_0) = \|x_0\|$, $\|F\| = 1$', fontsize=9)
ax.set_xlabel(r'$u$', fontsize=9); ax.set_ylabel(r'$v$', fontsize=9)
ax.tick_params(labelsize=8)
ax.legend(fontsize=7, loc='upper right')

plt.tight_layout()
plt.show()
```

*The functional $F(u,v) = u$ achieves $F(x_0) = \|x_0\|_\infty = 1.8$. The unit
ball fits inside the strip $|F| \leq 1$, and $x_0$ lies at exactly the right
height. This is separation of a point from the unit ball.*


````{prf:corollary} The sup formula
:label: hb-sup-formula

Let $X$ be a normed space and $B_{X^*} = \{f \in X^* : \|f\| \leq 1\}$ the closed unit ball of the dual. Then for all $x \in X$:

$$\|x\| = \sup\{|f(x)| : f \in B_{X^*}\} = \max\{|f(x)| : f \in B_{X^*}\}$$

In particular, the supremum is **attained**: there exists $f \in B_{X^*}$ with $|f(x)| = \|x\|$. The dual $X^*$ is a complete measurement system with no information loss.

```{prf:proof}
:class: dropdown

The inequality $\leq$: for any $f$ with $\|f\| \leq 1$, we have $|f(x)| \leq
\|f\|\|x\| \leq \|x\|$, so $\sup \leq \|x\|$.

The inequality $\geq$ (and that it is a max): by the {prf:ref}`norming property
<hb-norming>`, there exists $f \in X^*$ with $\|f\| = 1$ and $f(x) = \|x\|$.
This $f$ attains the supremum.
```
````

```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import matplotlib.pyplot as plt
from matplotlib.patches import Polygon

fig, ax = plt.subplots(figsize=(4.2, 3.3))

square_verts = np.array([[-1, -1], [1, -1], [1, 1], [-1, 1]])
sq = Polygon(square_verts, fill=True, facecolor='C0', alpha=0.1, edgecolor='C0', lw=2)
ax.add_patch(sq)

x0 = np.array([1.5, 1.0])
ax.plot(*x0, 'C3o', ms=7, zorder=5)
ax.text(x0[0]+0.05, x0[1]+0.15, r'$x_0$', fontsize=10, color='C3')

# Multiple functionals with their readings
functionals = [
    ((1, 0), r'$f_1 = u$', 'C1'),
    ((0, 1), r'$f_2 = v$', 'C2'),
    ((0.5, 0.5), r'$f_3 = \frac{u+v}{2}$', 'C4'),
]

y_text = -1.5
for (a, b), label, color in functionals:
    reading = a * x0[0] + b * x0[1]
    t = np.linspace(-2.5, 2.5, 200)
    if abs(b) > 0.01:
        for lev in [0, reading]:
            y_line = (lev - a * t) / b
            mask = (y_line > -2.5) & (y_line < 2.5)
            ls = '--' if abs(lev) < 0.01 else '-'
            ax.plot(t[mask], y_line[mask], color=color, alpha=0.5, lw=1.2, ls=ls)
    else:
        ax.axvline(0, color=color, alpha=0.5, lw=1.2, ls='--')
        ax.axvline(reading, color=color, alpha=0.5, lw=1.2)

    ax.text(1.8, y_text, f'{label}: {reading:.1f}', fontsize=7, color=color)
    y_text -= 0.35

ax.text(1.8, y_text - 0.1, r'$\|x_0\|_\infty = 1.5$', fontsize=8, fontweight='bold', color='C3')

ax.set_xlim(-2.6, 3.6)
ax.set_ylim(-2.6, 2.6)
ax.set_aspect('equal')
ax.set_title(r'The sup formula: $\|x_0\| = \max_{\|f\| \leq 1} |f(x_0)|$', fontsize=9)
ax.set_xlabel(r'$u$', fontsize=9); ax.set_ylabel(r'$v$', fontsize=9)
ax.tick_params(labelsize=8)

plt.tight_layout()
plt.show()
```

*Three unit-norm functionals give different "readings" of $x_0$: $f_1$ reads
$1.5$, $f_2$ reads $1.0$, $f_3$ reads $1.25$. The best reading equals
$\|x_0\|_\infty = 1.5$, and the norming property guarantees such an optimal
functional always exists. No information is lost: the dual is a complete
measurement system.*



````{prf:corollary} Classification of closures
:label: hb-closures

Let $M$ be a linear subspace of a normed space $X$ and let $x_0 \in X$. Then $x_0 \in \overline{M}$
if and only if there exists **no** bounded linear functional $f$ such that $f(x) = 0$ for all $x \in M$
but $f(x_0) \neq 0$.

```{prf:proof}
:class: dropdown

$(\Rightarrow)$ If $x_0 \in \overline{M}$, pick $x_n \in M$ with $x_n \to x_0$.
For any $f \in X^*$ vanishing on $M$, continuity gives $f(x_0) = \lim f(x_n) =
0$.

$(\Leftarrow)$ Suppose $x_0 \notin \overline{M}$. Then $\overline{M}$ is a
proper closed subspace and $d = \text{dist}(x_0, \overline{M}) > 0$. Define $g$
on $\overline{M} + \text{span}(x_0)$ by $g(m + \alpha x_0) = \alpha$.
Then $|g(m + \alpha x_0)| = |\alpha| \leq \|m + \alpha x_0\|/d$
(since $\|m + \alpha x_0\| \geq |\alpha| d$). So $\|g\| \leq 1/d$.
Hahn-Banach extends $g$ to $f \in X^*$. By construction $f = 0$ on $M$ but $f(x_0) = 1 \neq 0$.

```
````


```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import matplotlib.pyplot as plt

fig, axes = plt.subplots(1, 2, figsize=(14, 5.5))

# --- Panel 1: x0 in closure(M) ---
ax = axes[0]

# M = the x-axis (a 1D subspace in R^2)
ax.axhline(0, color='C0', lw=2.5, label=r'$M$ (subspace)')

# x0 on M (in the closure)
x0 = np.array([1.2, 0])
ax.plot(*x0, 'C3o', ms=10, zorder=5)
ax.text(x0[0]+0.1, x0[1]+0.15, r'$x_0 \in \overline{M}$', fontsize=13, color='C3')

# Show several functionals vanishing on M: any f with f=0 on M means f(u,v)=bv
# All have f(x0) = b * 0 = 0
for b_val, color in [(0.5, 'C4'), (1.0, 'C1'), (-0.7, 'C2')]:
    for c in [-1.5, -0.5, 0.5, 1.5]:
        ax.axhline(c / b_val if abs(b_val) > 0.01 else 0, color=color, alpha=0.15, lw=0.8)
    # The kernel (f=0 level set) is always the x-axis
    ax.axhline(0, color=color, alpha=0.3, lw=1.5, ls='--')
    label = rf'$f(u,v)={b_val}v$: $f(x_0)=0$'
    ax.text(2.1, 0.5 * b_val, label, fontsize=10, color=color)

ax.set_xlim(-2.5, 4.0)
ax.set_ylim(-2.5, 2.5)
ax.set_aspect('equal')
ax.set_title(r'$x_0 \in \overline{M}$: every $f$ vanishing on $M$' + '\nalso vanishes at $x_0$', fontsize=12)
ax.set_xlabel(r'$u$', fontsize=12); ax.set_ylabel(r'$v$', fontsize=12)
ax.legend(fontsize=11, loc='upper right')

# --- Panel 2: x0 not in closure(M) ---
ax = axes[1]

# M = the x-axis again
ax.axhline(0, color='C0', lw=2.5, label=r'$M$ (subspace)')

# x0 off M
x0 = np.array([0.8, 1.5])
ax.plot(*x0, 'C3o', ms=10, zorder=5)
ax.text(x0[0]+0.1, x0[1]+0.15, r'$x_0 \notin \overline{M}$', fontsize=13, color='C3')

# The separating functional: f(u,v) = v, which vanishes on M but f(x0) = 1.5
# Draw level sets of f(u,v) = v
for c in np.arange(-2, 2.5, 0.5):
    alpha = 0.5 if abs(c - 0) < 0.01 or abs(c - 1.5) < 0.01 else 0.15
    lw_val = 2.0 if abs(c - 0) < 0.01 or abs(c - 1.5) < 0.01 else 0.8
    color = 'C1' if abs(c - 1.5) < 0.01 else ('C0' if abs(c - 0) < 0.01 else 'gray')
    ax.axhline(c, color=color, alpha=alpha, lw=lw_val)

# Highlight the level set through x0
ax.axhline(x0[1], color='C1', lw=2, ls='--', alpha=0.7, label=rf'$f^{{-1}}({x0[1]})$: $f(x_0) = {x0[1]}$')

# Arrow showing distance
ax.annotate('', xy=(x0[0], 0), xytext=(x0[0], x0[1]),
            arrowprops=dict(arrowstyle='<->', color='C3', lw=1.5))
ax.text(x0[0]-0.5, x0[1]/2, r'$d > 0$', fontsize=12, color='C3')

ax.set_xlim(-2.5, 4.0)
ax.set_ylim(-2.5, 2.5)
ax.set_aspect('equal')
ax.set_title(r'$x_0 \notin \overline{M}$: Hahn-Banach finds $f$' + '\nwith $f|_M = 0$ but $f(x_0) \\neq 0$', fontsize=12)
ax.set_xlabel(r'$u$', fontsize=12); ax.set_ylabel(r'$v$', fontsize=12)
ax.legend(fontsize=11, loc='upper right')

plt.tight_layout()
plt.show()
```

*Left: $x_0$ lies in $\overline{M}$, so every functional that vanishes on $M$
also vanishes at $x_0$. No foliation can see a difference. Right: $x_0$ is at
positive distance from $M$, and Hahn-Banach produces a functional $f(u,v) = v$
that is zero on $M$ but reads $f(x_0) = 1.5 \neq 0$. The separating foliation
detects that $x_0$ is outside the closure.*


## Geometric Hahn–Banach: Separation of Convex Sets

The corollaries above separate points from points and points from the unit ball.
The **geometric form of Hahn–Banach** separates a point from any closed convex
set.

```{prf:theorem} Separation of point from closed convex set
:label: geometric-hahn-banach

Let $C \subset X$ be a closed convex set and $x_0 \notin C$. Then there exists $f \in X^*$ and a constant $\gamma$ such that

$$f(x_0) > \gamma \geq f(c) \quad \text{for all } c \in C$$

That is, there is a closed hyperplane $f^{-1}(\gamma)$ that **strictly separates** $x_0$ from $C$.
```

```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import matplotlib.pyplot as plt
from matplotlib.patches import Polygon, Ellipse

fig, axes = plt.subplots(1, 2, figsize=(12, 5))

# --- Panel 1: Separation from a convex set ---
ax = axes[0]

# Draw a convex "blob" (ellipse)
ellipse = Ellipse((-0.5, 0), 1.8, 1.2, angle=20, facecolor='C0', alpha=0.2,
                  edgecolor='C0', lw=2)
ax.add_patch(ellipse)
ax.text(-0.5, 0, r'$C$', fontsize=14, ha='center', va='center', color='C0')

# Point outside
x0 = np.array([1.5, 0.8])
ax.plot(*x0, 'C3o', ms=8, zorder=5)
ax.text(x0[0]+0.1, x0[1]+0.1, r'$x_0$', fontsize=13, color='C3')

# Separating hyperplane (a line)
# Normal direction pointing from C toward x0
normal = np.array([0.8, 0.3])
normal = normal / np.linalg.norm(normal)
gamma_pt = np.array([0.6, 0.4])  # point on the hyperplane

perp = np.array([-normal[1], normal[0]])
t = np.linspace(-3, 3, 100)
line = gamma_pt[:, None] + perp[:, None] * t[None, :]
ax.plot(line[0], line[1], 'C1-', lw=2, label=r'$f^{-1}(\gamma)$')

# Shade the side containing C
# Draw parallel level sets
for offset in [-0.5, -1.0, 0.5, 1.0]:
    shifted = gamma_pt + offset * normal
    line_s = shifted[:, None] + perp[:, None] * t[None, :]
    ax.plot(line_s[0], line_s[1], 'gray', alpha=0.2, lw=0.8)

ax.set_xlim(-2.5, 2.5)
ax.set_ylim(-2, 2)
ax.set_aspect('equal')
ax.set_title('Geometric Hahn–Banach:\nseparation from a closed convex set', fontsize=11)
ax.legend(fontsize=10, loc='lower right')
ax.set_xlabel(r'$x$'); ax.set_ylabel(r'$y$')

# --- Panel 2: Why convexity and closedness matter ---
ax = axes[1]

# Non-convex set: annulus
theta = np.linspace(0, 2*np.pi, 200)
r_out = 1.5
r_in = 0.5
ax.fill_between(r_out*np.cos(theta), r_out*np.sin(theta),
                alpha=0.2, color='C0')
ax.fill_between(r_in*np.cos(theta), r_in*np.sin(theta),
                alpha=1.0, color='white')
ax.plot(r_out*np.cos(theta), r_out*np.sin(theta), 'C0', lw=2)
ax.plot(r_in*np.cos(theta), r_in*np.sin(theta), 'C0', lw=2, ls='--')

ax.plot(0, 0, 'C3o', ms=8, zorder=5)
ax.text(0.1, 0.15, r'$x_0$', fontsize=13, color='C3')
ax.text(0, -1.0, r'$C$ (non-convex)', fontsize=11, ha='center', color='C0')

# Try to draw a line — it can't separate
ax.plot([-2, 2], [0, 0], 'C1--', lw=1.5, alpha=0.5, label='No line separates!')
ax.text(1.5, 0.15, '?', fontsize=16, color='C1', fontweight='bold')

ax.set_xlim(-2.2, 2.2)
ax.set_ylim(-2.2, 2.2)
ax.set_aspect('equal')
ax.set_title('Why convexity matters:\nnon-convex sets can surround a point', fontsize=11)
ax.legend(fontsize=10, loc='lower right')
ax.set_xlabel(r'$x$'); ax.set_ylabel(r'$y$')

plt.tight_layout()
plt.show()
```

### Why closedness and convexity matter

- **Closedness:** If $C$ is not closed, separation can fail. Consider $C = \{(x,
  y) : y > 0\} \cup \{(0, 0)\}$ and $x_0 = (1, 0)$. The point $x_0$ is not in
  $C$, but any separating line would need to separate from points arbitrarily
  close to the entire $x$-axis.

- **Convexity:** If $C$ is not convex, a hyperplane can't separate — it's a flat
  cut, and non-convex sets can wrap around a point.


## The Unit Ball as an Intersection of Strips

**What to do with this?**

The worked example in the previous section revealed many valid extensions — many
functionals, many foliations. We can turn this around and ask: **what does the
collection of all functionals tell us about the unit ball itself?**

Each unit-norm functional $f$ defines a **strip**: $S_f = \{x : |f(x)| \leq 1\}$
— the region between the level sets $f^{-1}(-1)$ and $f^{-1}(1)$. The norm
constraint $\|f\| = 1$ means the unit ball fits inside every such strip: $B_X
\subseteq S_f$.

By the {prf:ref}`sup formula <hb-sup-formula>`, the reverse holds too:

$$B_X = \bigcap_{f \in B_{X^*}} \{x : |f(x)| \leq 1\}$$

**The unit ball is exactly the intersection of all the strips.**

```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import matplotlib.pyplot as plt
from matplotlib.patches import Polygon, Rectangle

fig, axes = plt.subplots(1, 3, figsize=(15, 5))

# The dual of (R^2, l^infty) is (R^2, l^1)
# Extreme points of l^1 ball: (±1, 0), (0, ±1)

# Panel 1: Vertical strip from f = (1, 0)
ax = axes[0]
ax.axvspan(-1, 1, alpha=0.2, color='C0', label=r'$|x| \leq 1$')
ax.axvline(-1, color='C0', lw=2, alpha=0.7)
ax.axvline(1, color='C0', lw=2, alpha=0.7)
sq = Polygon([[-1,-1],[1,-1],[1,1],[-1,1]], fill=False, edgecolor='k', lw=2, ls='--')
ax.add_patch(sq)
ax.set_xlim(-2.2, 2.2)
ax.set_ylim(-2.2, 2.2)
ax.set_aspect('equal')
ax.set_title(r'Strip from $f = (1,0)$: $|x| \leq 1$', fontsize=11)
ax.legend(fontsize=10, loc='upper right')
ax.set_xlabel(r'$x$'); ax.set_ylabel(r'$y$')

# Panel 2: Horizontal strip from f = (0, 1)
ax = axes[1]
ax.axhspan(-1, 1, alpha=0.2, color='C1', label=r'$|y| \leq 1$')
ax.axhline(-1, color='C1', lw=2, alpha=0.7)
ax.axhline(1, color='C1', lw=2, alpha=0.7)
sq = Polygon([[-1,-1],[1,-1],[1,1],[-1,1]], fill=False, edgecolor='k', lw=2, ls='--')
ax.add_patch(sq)
ax.set_xlim(-2.2, 2.2)
ax.set_ylim(-2.2, 2.2)
ax.set_aspect('equal')
ax.set_title(r'Strip from $f = (0,1)$: $|y| \leq 1$', fontsize=11)
ax.legend(fontsize=10, loc='upper right')
ax.set_xlabel(r'$x$'); ax.set_ylabel(r'$y$')

# Panel 3: Intersection = the square
ax = axes[2]
# Show both strips lightly
ax.axvspan(-1, 1, alpha=0.1, color='C0')
ax.axhspan(-1, 1, alpha=0.1, color='C1')
# The intersection is the square
sq = Polygon([[-1,-1],[1,-1],[1,1],[-1,1]], fill=True, facecolor='C2',
             alpha=0.3, edgecolor='C2', lw=2.5, label=r'$B_X = $ intersection')
ax.add_patch(sq)
ax.axvline(-1, color='C0', lw=1.5, alpha=0.5, ls='--')
ax.axvline(1, color='C0', lw=1.5, alpha=0.5, ls='--')
ax.axhline(-1, color='C1', lw=1.5, alpha=0.5, ls='--')
ax.axhline(1, color='C1', lw=1.5, alpha=0.5, ls='--')
ax.set_xlim(-2.2, 2.2)
ax.set_ylim(-2.2, 2.2)
ax.set_aspect('equal')
ax.set_title(r'Intersection of strips $= B_{\ell^\infty}$', fontsize=11)
ax.legend(fontsize=10, loc='upper right')
ax.set_xlabel(r'$x$'); ax.set_ylabel(r'$y$')

plt.suptitle(r'The unit ball as intersection of dual strips (for $\ell^\infty$ on $\mathbb{R}^2$)',
             fontsize=13, y=1.02)
plt.tight_layout()
plt.show()
```

Other functionals in the dual ball (like $f = (1/2, 1/2)$, which gives
$|(x+y)/2| \leq 1$, i.e., $|x+y| \leq 2$) define wider strips that are
**redundant** — the square already fits inside them. The extreme functionals do
all the work.

**The general picture:** In a Banach space, the unit ball is "held in place" by
the collection of all dual strips. Each functional constrains from one
direction, and together they sculpt the ball. This is a preview of the **bipolar
theorem** and the **weak topology** — ideas that will return when we study weak
convergence and Banach–Alaoglu.

```{prf:remark} Strips, extensions, and the geometry of the unit ball
:class: dropdown

The formula $B_X = \bigcap_{\|f\| \leq 1} \{x : |f(x)| \leq 1\}$ uses strips from **all** unit-norm functionals in $X^*$, not just extensions of a single $f$ from a single subspace $M$.

In the Euclidean case ($\ell^2$), extending $f$ from $M$ gives a unique extension, hence a single strip. One strip between two parallel lines cannot carve out a circle. To recover the full $\ell^2$ ball, you need strips from many different subspaces, one per direction.

In the $\ell^\infty$ case, something striking happens: extending from the single subspace $M = \mathrm{span}(1,1)$ already produces a whole family of strips (parametrised by $c \in [-1,1]$), and their intersection is exactly the unit square. The non-uniqueness of Hahn–Banach does extra geometric work for free. One subspace suffices because the flat sides of the square allow enough freedom in the extension to generate all the constraints needed.
```


