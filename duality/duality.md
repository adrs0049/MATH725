---
kernelspec:
  name: python3
  display_name: Python 3
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/duality.pdf
    id: duality-duality-pdf
downloads:
  - id: duality-duality-pdf
    title: Download PDF
---

# The Dual Space

There are two methods to studying mathematical structures.

1. By looking at the objects **in** the space.
2. By looking at functions **on** the space.

Let's see how the second viewpoint looks in our Banach space setting.

## Introduction

In the Banach space setting the natural mappings to consider are the linear
continuous functions between two Banach spaces $X$ and $Y$. Now consider
$\mathcal{L}(X, \mathbb{R})$ the space of bounded linear continuous functionals
on $X$. This is a Banach space, and we will call it the **dual** of $X$ denoted
by $X^*$.

The intuitive view is that **functionals** are measurements of an object in the
space $X$.

```{prf:example}

We encounter many functionals in daily life.

1. A scale measures the weight of objects — it assigns a real number to each object.
2. A ruler measures length.
3. CT-scanners measure line integrals of an unknown tissue density.
4. MRI-scanners measure proton densities along lines.

```

## Isomorphisms and Isometries

First let's explore how we show that two Banach spaces have the same structure.
In normed vector spaces the **natural map** is $T : X \to Y$. $X$ and $Y$ are
equivalent if there exists an invertible continuous linear map $T : X \to Y$
i.e.

$$ c \|x\|_X \leq \|Tx\|_Y \leq C \|x\|_X $$

If such a map $T$ exists we say that $X$ and $Y$ are **isomorphic**. If $c = C =
1$ then $T$ is an **isometry**.

```{prf:remark}

The upper bound $\|Tx\|_Y \leq C\|x\|_X$ is simply the statement that $T$ is
bounded (continuous). The lower bound $c\|x\|_X \leq \|Tx\|_Y$ is equivalent to
$T^{-1}$ being bounded. By {prf:ref}`banach-inverse` (Banach's Bounded Inverse
Theorem), if $T : X \to Y$ is a **bijective** bounded linear map between Banach
spaces, then $T^{-1}$ is automatically bounded, so the lower bound comes **for
free**. In other words, to show two Banach spaces are isomorphic it suffices to
exhibit a bijective continuous linear map; one does not need to verify the lower
bound separately.
```


## The Finite-Dimensional Case

### Setup

Let $V = \mathbb{R}^n$ with the Euclidean norm $\|x\| = \sqrt{x_1^2 + \cdots +
x_n^2}$.

**Question:** What are the linear functionals $f : \mathbb{R}^n \to \mathbb{R}$?

Every such $f$ is of the form $f(y) = a \cdot y$ for some fixed vector $a \in
\mathbb{R}^n$.

```{prf:proof}
:nonumber:

If $e_1, \ldots, e_n$ is the standard basis, set $a_i = f(e_i)$. Then by linearity
$f(y) = \sum a_i y_i = a \cdot y$.
```


### The dual element of a vector

Given $x \in \mathbb{R}^n$, define the associated linear functional:

$$f_x(y) = x \cdot y$$

In matrix language: if vectors are columns, then $f_x$ acts as the row vector
$x^T$, so $f_x(y) = x^T y$.

**Key observations:**

- $f_x(x) = x \cdot x = \|x\|^2$ (evaluating the functional at the vector
  itself)
- $|f_x(y)| \leq \|x\|\|y\|$ by Cauchy–Schwarz
- The operator norm is $\|f_x\|_{\text{op}} = \sup_{\|y\|=1} |f_x(y)| = \|x\|$

The upper bound $\|f_x\|_{\text{op}} \leq \|x\|$ is Cauchy–Schwarz. For the
lower bound, plug in $y = x/\|x\|$:

$$f_x\!\left(\frac{x}{\|x\|}\right) = \frac{x \cdot x}{\|x\|} = \|x\|$$

So the map $x \mapsto f_x$ is an **isometric isomorphism** $\mathbb{R}^n
\xrightarrow{\sim} (\mathbb{R}^n)^*$.

```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import matplotlib.pyplot as plt
from matplotlib.patches import FancyArrowPatch

fig, ax = plt.subplots(1, 1, figsize=(6, 5))

# Show the dual pairing in R^2
# Vector x and its dual functional f_x
x = np.array([1.5, 1.0])
x_norm = np.linalg.norm(x)

# Draw unit circle
theta = np.linspace(0, 2*np.pi, 200)
ax.plot(np.cos(theta), np.sin(theta), 'k-', alpha=0.3, linewidth=1)

# Draw the vector x
ax.annotate('', xy=x, xytext=(0, 0),
            arrowprops=dict(arrowstyle='->', color='C0', lw=2))
ax.text(x[0]+0.08, x[1]+0.08, r'$x$', fontsize=14, color='C0')

# Draw x/||x|| on the unit circle
x_hat = x / x_norm
ax.annotate('', xy=x_hat, xytext=(0, 0),
            arrowprops=dict(arrowstyle='->', color='C1', lw=2))
ax.text(x_hat[0]+0.08, x_hat[1]-0.15, r'$x/\|x\|$', fontsize=12, color='C1')

# Draw the level sets of f_x: these are lines perpendicular to x
# f_x(y) = x · y = c  =>  direction perpendicular to x
perp = np.array([-x[1], x[0]])  # perpendicular direction
perp = perp / np.linalg.norm(perp)

for c_val in [-5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5]:
    # Point on the level set: project onto x direction
    base = (c_val / x_norm**2) * x
    t = np.linspace(-3, 3, 100)
    line = base[:, None] + perp[:, None] * t[None, :]
    alpha = 0.6 if c_val == 0 else 0.3
    lw = 1.5 if c_val == 0 else 1
    ax.plot(line[0], line[1], 'gray', alpha=alpha, lw=lw)
    # Label
    label_pos = base + 1.6 * perp
    if -2.2 < label_pos[0] < 2.2 and -2.2 < label_pos[1] < 2.2:
        ax.text(label_pos[0], label_pos[1], f'$f_x = {c_val}$',
                fontsize=9, color='gray', ha='center')

ax.set_xlim(-2.2, 2.2)
ax.set_ylim(-2.2, 2.2)
ax.set_aspect('equal')
ax.axhline(0, color='k', lw=0.5, alpha=0.3)
ax.axvline(0, color='k', lw=0.5, alpha=0.3)
ax.set_title(r'The dual functional $f_x(y) = x \cdot y$ and its level sets', fontsize=12)
ax.set_xlabel(r'$y_1$')
ax.set_ylabel(r'$y_2$')
plt.tight_layout()
plt.show()
```

### Properties of the finite-dimensional dual

````{prf:proposition}
:label: finite-dim-dual-properties

In $\mathbb{R}^n$ the following hold:

1. **Every linear functional is continuous.** A linear map $f: \mathbb{R}^n \to \mathbb{R}$ is automatically bounded. There is no gap between the algebraic dual and the topological dual: $V' = X^*$.

2. **Extension is immediate.** If $f$ is defined on a subspace $M \subset \mathbb{R}^n$, extend it to all of $\mathbb{R}^n$ by choosing a complementary basis. No axiom of choice required.

3. **The sup formula holds.** For any $x \in \mathbb{R}^n$:
   $$\|x\| = \max_{\|f\|_{\text{op}} \leq 1} |f(x)|$$
   Take $f = f_{x/\|x\|}$ to achieve the max. The norm is fully recovered from the dual.

4. **$X^*$ separates points.** If $f(x) = f(y)$ for all $f \in (\mathbb{R}^n)^*$, then $x = y$.

```{prf:proof}
:class: dropdown

We prove property 4. By linearity, $f(x-y) = 0$ for all $f$. Take $f = f_{x-y}$, the functional $f_{x-y}(v) = (x-y) \cdot v$. Then
$0 = f_{x-y}(x-y) = (x-y)\cdot(x-y) = \|x-y\|^2$, so $x = y$.
```
````

The key observation is that given any vector we want to detect, the inner
product lets us immediately build the right functional. In infinite dimensions
we no longer have this luxury, and constructing functionals with prescribed
behavior requires the **Hahn-Banach theorem**.


## What Goes Wrong in Infinite Dimensions?

### Algebraic vs. topological dual

Let $X = (V, \|\cdot\|)$ be a normed space, with $V$ a vector space over
$\mathbb{R}$.

```{prf:definition} Algebraic dual
$V'$ is the set of *all* linear functionals $f : V \to \mathbb{R}$ — no continuity requirement. This is a purely algebraic object.
```

```{prf:definition} Topological dual
:label: topological-dual

$X^* \subset V'$ is the set of all *bounded* (equivalently, continuous) linear functionals $f : V \to \mathbb{R}$, equipped with the operator norm:
$$\|f\|_{X^*} = \|f\|_{\text{op}} = \sup_{\|x\| \leq 1} |f(x)|$$
$X^*$ is always a Banach space (even if $X$ itself is not complete).
```

In infinite dimensions, $V' \supsetneq X^*$ — there exist discontinuous linear
functionals. These are constructed via a Hamel basis (using Zorn's lemma / axiom
of choice), and they are thoroughly pathological: unbounded on every
neighborhood of $0$.

### Could the topological dual be trivial?

Could $X^*$ be trivially small? We know $V' \neq \{0\}$
(Hamel basis argument), but these algebraic functionals are useless for
analysis. Could it happen that $X^* = \{0\}$ — that the *only* continuous linear
functional is the zero functional?

If $X^* = \{0\}$, we cannot distinguish elements via functionals and there is no useful duality theory.

**This happens!** The spaces $L^p(\Omega)$ for $0 < p < 1$ have trivial
dual: $(L^p)^* = \{0\}$. These are complete metric spaces (F-spaces) but not
Banach spaces. The idea (due to Day {cite}`day1940`) is simple: one shows that $L^p$ for
$0 < p < 1$ has **no proper convex open subsets**. But any nonzero continuous
linear functional $f$ would make $\{x : |f(x)| < 1\}$ exactly such a set, so
no such $f$ can exist.

This motivates why **Banach spaces** (with their convex unit balls) are the
right setting for duality.


### The dual as a measurement system

Here is the motivating picture for the rest of this chapter.

Suppose you have an element $x \in X$ and you want to know its norm $\|x\|$. But
you're not allowed to compute $\|x\|$ directly — instead, you can only **probe**
$x$ using continuous linear functionals. Each $f \in X^*$ with $\|f\| \leq 1$
gives you a **reading** $|f(x)|$. Think of these as measurement instruments:
each one returns a number, and you take the supremum over all available
instruments:

$$\text{best reading} = \sup\{|f(x)| : f \in B_{X^*}\}$$

One inequality is trivial: since $|f(x)| \leq \|f\|\|x\| \leq \|x\|$ for any $f$
in the unit ball of $X^*$, no instrument ever reads **too high**:

$$\sup\{|f(x)| : f \in B_{X^*}\} \leq \|x\|$$

But the real worry is the other direction: **could all your instruments read too
low?** Could there be some "hidden size" in $x$ that no continuous functional
detects? If so, there is a gap between what the dual can see and what is
actually there.

In finite dimensions this can't happen: the functional $f_{x/\|x\|}$ gives a
reading of exactly $\|x\|$. But in infinite dimensions, we don't know *a priori*
that such an optimal instrument exists.

If $X^* = \{0\}$ (as for $L^p$ with $0 < p < 1$), the situation is as bad as
possible: the supremum is $0$ for every nonzero $x$. The dual sees nothing.

**The question Hahn–Banach answers:** Is $X^*$ a **complete measurement system**,
one with no information loss? That is, do we have

$$\|x\| = \max\{|f(x)| : f \in B_{X^*}\}?$$

The answer is **yes** for all Banach spaces: the sup is attained, and the dual
recovers the full norm.
