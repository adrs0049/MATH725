---
kernelspec:
  name: python3
  display_name: Python 3
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/hilbert-probability.pdf
    id: introduction-hilbert-probability-pdf
downloads:
  - id: introduction-hilbert-probability-pdf
    title: Download PDF
---

# Hilbert Spaces and the Geometry of Probability

A Banach space becomes considerably richer when its norm comes from an inner
product. The resulting structure, a **Hilbert space**, gives us orthogonality,
projections, and angles. The payoff is immediate: the entire machinery of
probability (expectation, variance, correlation, conditional expectation) turns
out to be Hilbert space geometry in disguise.


## Hilbert spaces

```{prf:definition} Inner product space
:label: def-inner-product

An **inner product** on a real vector space $X$ is a map $\langle \cdot, \cdot
\rangle : X \times X \to \mathbb{R}$ satisfying

1. *Symmetry:* $\langle x, y \rangle = \langle y, x \rangle$
2. *Linearity:* $\langle \alpha x + \beta y, z \rangle = \alpha \langle x, z
   \rangle + \beta \langle y, z \rangle$
3. *Positive definiteness:* $\langle x, x \rangle \geq 0$, with equality iff
   $x = 0$

Every inner product induces a norm $\|x\| = \sqrt{\langle x, x \rangle}$.
```

```{prf:definition} Hilbert space
:label: def-hilbert

A **Hilbert space** is a complete inner product space: a Banach space whose norm
is induced by an inner product.
```

```{prf:example} Finite-dimensional examples
:label: ex-hilbert-finite

$\mathbb{R}^n$ with $\langle x, y \rangle = \sum_{i=1}^n x_i y_i$ is a Hilbert
space. Any finite-dimensional inner product space is automatically complete.
```

```{prf:example} $\ell^2$ and $L^2$
:label: ex-hilbert-l2

The sequence space $\ell^2 = \{(x_n) : \sum |x_n|^2 < \infty\}$ with
$\langle x, y \rangle = \sum x_n y_n$ is a Hilbert space.

For a measure space $(\Omega, \mu)$, the function space $L^2(\Omega, \mu)$ with

$$
\langle f, g \rangle = \int_\Omega f \, g \, d\mu
$$

is a Hilbert space. This is the inner product that was already implicit in the
Fourier series from {doc}`/introduction/intro`.
```

The key additional structure that an inner product provides is **orthogonality**:
we say $x \perp y$ when $\langle x, y \rangle = 0$.

```{prf:theorem} Cauchy-Schwarz inequality
:label: thm-cauchy-schwarz

For all $x, y$ in an inner product space,

$$
|\langle x, y \rangle| \leq \|x\| \, \|y\|
$$

with equality iff $x$ and $y$ are linearly dependent.
```

This lets us define the **angle** between nonzero vectors:

$$
\cos \theta = \frac{\langle x, y \rangle}{\|x\| \, \|y\|}.
$$

```{prf:remark} Which $L^p$ spaces are Hilbert?
:class: dropdown

Among $L^p$ spaces, **only $p = 2$** gives a Hilbert space. For $p \neq 2$, the
$L^p$ norm does not satisfy the parallelogram law $\|f+g\|^2 + \|f-g\|^2 =
2\|f\|^2 + 2\|g\|^2$, which is necessary and sufficient for a norm to come from
an inner product (the Jordan-von Neumann theorem). This is why $L^2$ occupies a
special place in analysis.
```


## Orthogonal projection

The most important consequence of the Hilbert space structure is the projection
theorem.

````{prf:theorem} Orthogonal projection
:label: thm-orthogonal-projection

Let $H$ be a Hilbert space and $M \subset H$ a **closed** subspace. For every
$x \in H$, there exists a unique $\hat{x} \in M$ such that

$$
\|x - \hat{x}\| = \inf_{m \in M} \|x - m\|.
$$

This $\hat{x}$ is called the **orthogonal projection** of $x$ onto $M$ and is
characterized by

$$
x - \hat{x} \perp M, \qquad \text{i.e.} \quad \langle x - \hat{x}, m \rangle = 0 \;\; \text{for all } m \in M.
$$

```{prf:proof}
:class: dropdown

**Existence.** Let $d = \inf_{m \in M} \|x - m\|$ and pick a minimizing sequence
$m_n \in M$ with $\|x - m_n\| \to d$. The parallelogram law gives

$$
\|m_n - m_k\|^2 = 2\|x - m_n\|^2 + 2\|x - m_k\|^2 - 4\left\|x - \frac{m_n + m_k}{2}\right\|^2 \leq 2\|x - m_n\|^2 + 2\|x - m_k\|^2 - 4d^2
$$

since $(m_n + m_k)/2 \in M$. As both $\|x - m_n\|^2$ and $\|x - m_k\|^2$ tend
to $d^2$, the right side tends to $0$, so $(m_n)$ is Cauchy. By completeness,
$m_n \to \hat{x} \in M$ (since $M$ is closed), and $\|x - \hat{x}\| = d$.

**Orthogonality.** For any $m \in M$ and $t \in \mathbb{R}$, $\hat{x} + tm \in
M$, so

$$
\|x - \hat{x}\|^2 \leq \|x - \hat{x} - tm\|^2 = \|x - \hat{x}\|^2 - 2t\langle x - \hat{x}, m \rangle + t^2\|m\|^2.
$$

This gives $0 \leq -2t\langle x - \hat{x}, m \rangle + t^2\|m\|^2$ for all $t$,
which forces $\langle x - \hat{x}, m \rangle = 0$.

**Uniqueness.** If $\hat{x}_1, \hat{x}_2$ are both minimizers, then $\hat{x}_1
- \hat{x}_2 \in M$ and $\langle x - \hat{x}_1, \hat{x}_1 - \hat{x}_2 \rangle =
0$. Similarly $\langle x - \hat{x}_2, \hat{x}_1 - \hat{x}_2 \rangle = 0$.
Subtracting: $\|\hat{x}_1 - \hat{x}_2\|^2 = 0$.
```
````

```{prf:remark}
:class: dropdown

The projection theorem **fails** in general Banach spaces: the closest point in
a closed subspace may not exist or may not be unique. The parallelogram law is
used in an essential way to show the minimizing sequence is Cauchy. This is one
of the main reasons Hilbert spaces are easier to work with than general Banach
spaces.
```


## Application: Probability as Hilbert space geometry

Fix a probability space $(\Omega, \mathcal{F}, P)$. The space of
**square-integrable random variables**

$$
L^2(\Omega, P) = \left\{X : \Omega \to \mathbb{R} \text{ measurable} : \mathbb{E}[X^2] < \infty\right\} \big/ \!\sim
$$

is a Hilbert space with inner product $\langle X, Y \rangle = \mathbb{E}[XY]$.
Every familiar concept in probability is a geometric operation in this space.

### Expectation, variance, and correlation

```{prf:proposition} Probabilistic concepts as geometry
:label: prop-prob-geometry

Let $X, Y \in L^2(\Omega, P)$ and write $\tilde{X} = X - \mathbb{E}[X]$ for the
centered version. Then:

1. **Expectation** is an inner product: $\mathbb{E}[X] = \langle X, \mathbf{1} \rangle$.
2. **Variance** is a squared norm: $\operatorname{Var}(X) = \|\tilde{X}\|^2$.
3. **Covariance** is an inner product: $\operatorname{Cov}(X, Y) = \langle \tilde{X}, \tilde{Y} \rangle$.
4. **Correlation** is a cosine:
   $\rho(X, Y) = \cos \theta = \frac{\langle \tilde{X}, \tilde{Y} \rangle}{\|\tilde{X}\| \, \|\tilde{Y}\|}$.
5. **Uncorrelated** means **orthogonal**: $\operatorname{Cov}(X, Y) = 0 \iff \tilde{X} \perp \tilde{Y}$.
```

The Cauchy-Schwarz inequality immediately gives $|\rho(X,Y)| \leq 1$, with
equality iff $Y$ is an affine function of $X$.

```{prf:example} Pythagorean theorem for variance
:label: ex-pythagorean-var

If $X_1, \ldots, X_n$ are pairwise uncorrelated, then

$$
\operatorname{Var}\left(\sum_{i=1}^n X_i\right) = \sum_{i=1}^n \operatorname{Var}(X_i).
$$

This is the Pythagorean theorem $\|\tilde{X}_1 + \cdots + \tilde{X}_n\|^2 =
\|\tilde{X}_1\|^2 + \cdots + \|\tilde{X}_n\|^2$ applied to orthogonal vectors.
```


### Conditional expectation as orthogonal projection

This is the deepest connection between probability and Hilbert space geometry.

Given a sub-$\sigma$-algebra $\mathcal{G} \subset \mathcal{F}$, the space

$$
L^2(\mathcal{G}) = \{X \in L^2(\mathcal{F}) : X \text{ is } \mathcal{G}\text{-measurable}\}
$$

is a **closed subspace** of $L^2(\mathcal{F})$.

````{prf:theorem} Conditional expectation is projection
:label: thm-cond-exp-proj

For any $X \in L^2(\mathcal{F})$, the conditional expectation
$\mathbb{E}[X \mid \mathcal{G}]$ is the orthogonal projection of $X$ onto
$L^2(\mathcal{G})$:

$$
\mathbb{E}[X \mid \mathcal{G}] = \operatorname{proj}_{L^2(\mathcal{G})} X = \arg\min_{Y \in L^2(\mathcal{G})} \mathbb{E}[(X - Y)^2].
$$

It is characterized by:
1. $\mathbb{E}[X \mid \mathcal{G}]$ is $\mathcal{G}$-measurable.
2. $X - \mathbb{E}[X \mid \mathcal{G}] \perp L^2(\mathcal{G})$, i.e.
   $\mathbb{E}[(X - \mathbb{E}[X \mid \mathcal{G}]) Z] = 0$ for all
   $Z \in L^2(\mathcal{G})$.

```{prf:proof}
:class: dropdown

$L^2(\mathcal{G})$ is a closed subspace of the Hilbert space
$L^2(\mathcal{F})$, so the {prf:ref}`projection theorem
<thm-orthogonal-projection>` gives existence and uniqueness of the minimizer
$\hat{X} = \operatorname{proj}_{L^2(\mathcal{G})} X$, characterized by
$\langle X - \hat{X}, Z \rangle = 0$ for all $Z \in L^2(\mathcal{G})$.

Taking $Z = \mathbf{1}_G$ for $G \in \mathcal{G}$, this reads $\int_G X \, dP =
\int_G \hat{X} \, dP$ for all $G \in \mathcal{G}$, which is the classical
definition of conditional expectation.
```
````

All standard properties of conditional expectation follow from the fact that it
is an orthogonal projection:

- **Idempotent:** $\mathbb{E}[\mathbb{E}[X \mid \mathcal{G}] \mid \mathcal{G}] = \mathbb{E}[X \mid \mathcal{G}]$ (projecting twice does nothing).
- **Contractive:** $\|\mathbb{E}[X \mid \mathcal{G}]\| \leq \|X\|$ (projections don't increase norms).
- **Tower property:** if $\mathcal{H} \subset \mathcal{G}$ then
  $\mathbb{E}[\mathbb{E}[X \mid \mathcal{G}] \mid \mathcal{H}] = \mathbb{E}[X \mid \mathcal{H}]$
  (composing projections onto nested subspaces gives the smaller projection).
- **Variance decomposition:**
  $\operatorname{Var}(X) = \mathbb{E}[\operatorname{Var}(X \mid \mathcal{G})] + \operatorname{Var}(\mathbb{E}[X \mid \mathcal{G}])$
  (the Pythagorean theorem).


### Regression as projection

When you condition on a random variable $Y$, the subspace $L^2(\sigma(Y))$
consists of all random variables that can be computed from $Y$ alone (i.e.,
functions $g(Y)$). The conditional expectation

$$
\mathbb{E}[X \mid Y] = \arg\min_{g} \mathbb{E}[(X - g(Y))^2]
$$

finds the function of $Y$ that best predicts $X$ in mean-squared error. This is
**nonparametric regression**. Restricting to linear functions $g(y) = a + by$
gives **linear regression**, which is projection onto a two-dimensional subspace.

```{prf:example} Linear regression from orthogonality
:label: ex-linear-regression

The best linear predictor $\hat{X} = a + bY$ satisfies $X - \hat{X} \perp
\{1, Y\}$, giving

$$
b = \frac{\operatorname{Cov}(X, Y)}{\operatorname{Var}(Y)}, \qquad a = \mathbb{E}[X] - b\,\mathbb{E}[Y].
$$

The prediction is

$$
\hat{X} = \mathbb{E}[X] + \rho \frac{\sigma_X}{\sigma_Y}(Y - \mathbb{E}[Y])
$$

where $\rho = \operatorname{Cor}(X,Y)$. When $|\rho| < 1$, the prediction
**shrinks** toward the mean: extreme observations of $Y$ produce less extreme
predictions of $X$.
```
