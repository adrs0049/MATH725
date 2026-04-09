---
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/structure.pdf
    id: distributions-structure-pdf
downloads:
  - id: distributions-structure-pdf
    title: Download PDF
---

# Support and Locality

## Support of a Distribution

A distribution $T$ is said to be supported in a closed set $K$ if $\langle T, \phi \rangle = 0$
for all $\phi \in \mathcal{C}_c^{\infty}(\mathbb{R}^d)$ with
$\text{supp}(\phi) \cap K = \emptyset$.

The support of $T$, denoted $\text{supp}(T)$, is the smallest set $K$ such that $T$ is supported
in $K$.

```{prf:example}

- The support of the Dirac delta is $\text{supp}(\delta) = \{ 0 \} $.
- If $f$ is a continuous function, $\text{supp}(T_f) = \overline{\{ x : f(x) \neq 0 \}}$.

```

## Local Structure

Two distributions $T_1$ and $T_2$ are equal on an open set $\Omega$ if
$\langle T_1, \phi \rangle = \langle T_2, \phi \rangle$ for all $\phi$.

If $T_f$ is a regular distribution and $T_f = 0$ on an open set $\Omega$, then $f = 0$
almost everywhere on $\Omega$.

## Distributions with Point Support

A fundamental result: If $T$ is a distribution supported at a single point $x_0$, then
$T$ is a finite linear combination of derivatives of the delta function at $x_0$:

$$
    T = \sum_{|\alpha| \leq m} c_{\alpha} D^\alpha \delta_{x_0}
$$

where $m$ is the order of $T$.


# The Structure Theorem for Distributions

The results above characterize distributions with *point* support. The
structure theorem generalizes this to *all* distributions: every
distribution is, locally, a finite-order derivative of a continuous function.

```{prf:theorem} Structure theorem for distributions
:label: structure-theorem-distributions

Let $T \in \mathcal{D}'(\Omega)$ and let $K \subset \Omega$ be compact.
Then there exist an integer $N \geq 0$ and continuous functions
$f_\alpha \in C(K)$, $|\alpha| \leq N$, such that

$$T = \sum_{|\alpha| \leq N} D^\alpha f_\alpha \qquad \text{on a neighborhood of } K.$$

If $T$ has finite order $m$ globally (i.e., the seminorm bound
$|\langle T, \varphi \rangle| \leq C_K \sum_{|\alpha| \leq m}
\sup |D^\alpha \varphi|$ holds with the same $m$ for all compact $K$),
then we can take $N = m$ uniformly.
```

```{prf:proof}
:class: dropdown

We sketch the argument in one dimension for clarity; the general case is
identical in structure.

**Step 1: From the order bound to a norm estimate.**
On a compact set $K$, the distribution $T$ has some finite order $m$:

$$|\langle T, \varphi \rangle| \leq C_K \sum_{k=0}^{m} \|\varphi^{(k)}\|_\infty \qquad \text{for all } \varphi \in \mathcal{D}_K.$$

This means $T$ is a continuous linear functional on $\mathcal{D}_K$
equipped with the $C^m$ norm.

**Step 2: Extension to a continuous linear functional.**
The space $\mathcal{D}_K$ is a subspace of $C^m(K)$. By the Hahn-Banach
theorem, $T$ extends to a continuous linear functional on $C^m(K)$.

**Step 3: Representation via antiderivatives.**
A continuous linear functional on $C^m(K)$ can be written as a finite sum
of integrals against Radon measures $\mu_\alpha$, $|\alpha| \leq m$:

$$\langle T, \varphi \rangle = \sum_{|\alpha| \leq m} \int D^\alpha \varphi \, d\mu_\alpha.$$

Each Radon measure $\mu_\alpha$ on a compact subset of $\mathbb{R}^d$ has a
continuous antiderivative: there exists $f_\alpha \in C(K)$ such that
$\int \psi \, d\mu_\alpha = (-1)^{|\alpha|} \int f_\alpha \, D^\alpha \psi \, dx$
for test functions $\psi$. (In one dimension, this is just the fact that
the antiderivative of a measure is a function of bounded variation, and
one more antiderivative gives a continuous function.) Substituting:

$$\langle T, \varphi \rangle = \sum_{|\alpha| \leq N} (-1)^{|\alpha|} \int f_\alpha \, D^\alpha \varphi \, dx = \sum_{|\alpha| \leq N} \langle D^\alpha f_\alpha, \varphi \rangle$$

where $N = m + d$ accounts for the additional antiderivatives needed in
$d$ dimensions.
```

```{prf:remark} Distributions are derivatives of continuous functions
:label: remark-structure-meaning
:class: dropdown

The structure theorem demystifies distributions: no matter how singular
a distribution may appear, it is always locally a finite sum of
derivatives of continuous functions. The Dirac delta is $H'$ (derivative
of the Heaviside function, which is bounded and measurable — or the
second derivative of the continuous function $\max(x,0)$). The derivative
$\delta'$ is the third derivative of $\max(x,0)$. And so on.

The price of increased singularity is simply a higher derivative order, not
a fundamentally different kind of object.
```

The structure theorem immediately implies the point support result stated
above:

```{prf:corollary}
:label: point-support-corollary

If $T \in \mathcal{D}'(\mathbb{R}^d)$ with $\operatorname{supp}(T) = \{x_0\}$,
then $T = \sum_{|\alpha| \leq m} c_\alpha D^\alpha \delta_{x_0}$.
```

```{prf:proof}
:class: dropdown

By the structure theorem, on a ball $B$ around $x_0$, we have
$T = \sum_{|\alpha| \leq N} D^\alpha f_\alpha$ for continuous $f_\alpha$.
Since $\operatorname{supp}(T) = \{x_0\}$, the distribution $T$ vanishes
on $B \setminus \{x_0\}$, which means each $f_\alpha$ is a polynomial of
degree at most $N - |\alpha|$ on $B \setminus \{x_0\}$, and by continuity
on all of $B$. A polynomial supported at a point must be constant times a
suitable derivative of $\delta_{x_0}$. Collecting terms gives
$T = \sum_{|\alpha| \leq m} c_\alpha D^\alpha \delta_{x_0}$ where
$m \leq N$ is the order of $T$.
```

