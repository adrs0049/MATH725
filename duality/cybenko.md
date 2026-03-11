---
kernelspec:
  name: python3
  display_name: Python 3
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/cybenko.pdf
    id: duality-cybenko-pdf
downloads:
  - id: duality-cybenko-pdf
    title: Download PDF
---

# Application: The Universal Approximation Theorem

We give a clean application of the Hahn-Banach theorem to neural networks:
Cybenko's proof {cite}`cybenko1989` that single-hidden-layer networks are dense
in $C(\Omega)$.

## Single-hidden-layer networks

Fix $\Omega = [0,1]^d$ and an activation function $\sigma : \mathbb{R} \to
\mathbb{R}$. A **single-hidden-layer network** with $M$ neurons is a function of
the form

$$
f(x) = \sum_{j=1}^{M} a_j \, \sigma(w_j \cdot x + b_j), \quad x \in \mathbb{R}^d
$$

where $w_j \in \mathbb{R}^d$ are weights, $b_j \in \mathbb{R}$ are biases, and
$a_j \in \mathbb{R}$ are output coefficients. The set of all such functions
(for all $M$) forms a linear subspace of $C(\Omega)$:

$$
\mathcal{N}_\sigma = \operatorname{span}\{\sigma(w \cdot x + b) : w \in \mathbb{R}^d,\; b \in \mathbb{R}\} \subset C(\Omega).
$$

```{prf:definition} Universal approximator
:label: def-universal-approximator

An activation function $\sigma$ is a **universal approximator** if
$\mathcal{N}_\sigma$ is dense in $C(\Omega)$, i.e.
$\overline{\mathcal{N}_\sigma} = C(\Omega)$.
```

**The question:** Which activations $\sigma$ are universal approximators?

## Discriminatory activations

```{prf:definition} Discriminatory function
:label: def-discriminatory

A continuous function $\sigma : \mathbb{R} \to \mathbb{R}$ is
**discriminatory** if, for any finite signed Borel measure $\mu$ on $\Omega$,

$$
\int_\Omega \sigma(w \cdot x + b) \, d\mu(x) = 0 \quad \text{for all } w \in \mathbb{R}^d,\; b \in \mathbb{R}
$$

implies $\mu = 0$.
```

In other words, no nonzero measure can be invisible to every neuron
$\sigma(w \cdot x + b)$.


## Cybenko's theorem

````{prf:theorem} Universal Approximation (Cybenko, 1989)
:label: thm-cybenko

Let $\sigma : \mathbb{R} \to \mathbb{R}$ be continuous and discriminatory. Then

$$
\overline{\mathcal{N}_\sigma} = C(\Omega).
$$

```{prf:proof}
:class: dropdown

Suppose for contradiction that $\overline{\mathcal{N}_\sigma} \neq C(\Omega)$.

**Step 1 (Hahn-Banach).** Since $\overline{\mathcal{N}_\sigma}$ is a proper
closed subspace, the {prf:ref}`classification of closures <hb-closures>`
gives a nonzero $F \in C(\Omega)^*$ with $F = 0$ on $\mathcal{N}_\sigma$.

**Step 2 (Riesz-Markov).** By the
{prf:ref}`Riesz-Markov-Kakutani theorem <riesz-markov>`, there is a unique
nonzero signed measure $\mu$ on $\Omega$ with

$$
F(\phi) = \int_\Omega \phi \, d\mu \quad \text{for all } \phi \in C(\Omega).
$$

**Step 3 (Contradiction).** Since $F$ vanishes on $\mathcal{N}_\sigma$, we have

$$
\int_\Omega \sigma(w \cdot x + b) \, d\mu(x) = 0 \quad \text{for all } w,\; b.
$$

Because $\sigma$ is discriminatory, $\mu = 0$, contradicting $F \neq 0$.
```
````


## Which activations are discriminatory?

The definition asks that no nonzero measure hides from every neuron. The key
observation is that steep rescalings of $\sigma$ approximate indicator functions
of half-spaces.

````{prf:proposition} Sigmoidal activations are discriminatory
:label: prop-sigmoid-discriminatory

Any bounded measurable function $\sigma$ with

$$
\sigma(t) \to \begin{cases} 1 & t \to +\infty \\ 0 & t \to -\infty \end{cases}
$$

is discriminatory.

```{prf:proof}
:class: dropdown

For $\lambda > 0$, the rescaled neuron $\sigma(\lambda(w \cdot x + b))$
converges pointwise as $\lambda \to \infty$ to the half-space indicator

$$
\mathbf{1}_{H_{w,b}}(x), \qquad H_{w,b} = \{x : w \cdot x + b > 0\}.
$$

If $\int \sigma(w \cdot x + b) \, d\mu = 0$ for all $w, b$, then the same
holds for $\sigma(\lambda(w \cdot x + b))$ (replace $w$ by $\lambda w$ and $b$
by $\lambda b$). Dominated convergence gives

$$
\mu(H_{w,b}) = \int \mathbf{1}_{H_{w,b}} \, d\mu = 0 \quad \text{for all half-spaces } H_{w,b}.
$$

Half-spaces generate the Borel $\sigma$-algebra on $\Omega$, so $\mu = 0$.
```
````

````{prf:proposition} ReLU is discriminatory
:label: prop-relu-discriminatory

The ReLU activation $\sigma(t) = \max(0, t)$ is discriminatory.

```{prf:proof}
:class: dropdown

For any $w, b$ and $\lambda > 0$, note that

$$
\frac{1}{\lambda}\bigl[\operatorname{ReLU}(\lambda(w \cdot x + b)) - \operatorname{ReLU}(\lambda(w \cdot x + b) - 1)\bigr] \to \mathbf{1}_{H_{w,b}}(x)
$$

pointwise as $\lambda \to \infty$. Since $\int \operatorname{ReLU}(w \cdot x +
b) \, d\mu = 0$ for all $w, b$, the same dominated convergence argument gives
$\mu(H_{w,b}) = 0$ for all half-spaces, hence $\mu = 0$.
```
````


Compare this with the {prf:ref}`Weierstrass theorem <ex-weierstrass>` from our
discussion of {doc}`/introduction/approximation`: polynomials are dense in
$C([a,b])$, and Cybenko's theorem says the same for neural networks in
$C([0,1]^d)$. Both are density results, but there is an important difference.
Weierstrass approximation suffers from the **curse of dimensionality**: the
number of monomials of degree $\leq n$ in $d$ variables grows as
$\binom{n+d}{d}$, which is exponential in $d$. Neural networks avoid this; the
approximation is built from neurons $\sigma(w \cdot x + b)$ that each cut across
all $d$ dimensions simultaneously, so the number of terms needed can scale much
more favourably with $d$.

On the other hand, the proof is non-constructive (it rests on Hahn-Banach, which
uses Zorn's lemma), so it says nothing about **how many neurons** are needed for
a given accuracy $\varepsilon$or **how to find the weights**.


## A second strategy for density proofs

In the {doc}`/introduction/approximation` chapter, every density proof was
**constructive**: we built an explicit approximating sequence (Bernstein
polynomials for Weierstrass, mollifiers for $C_c^\infty \subset L^p$) and
estimated the error directly. Cybenko's proof is fundamentally different. Instead
of constructing an approximation, it argues by contradiction via duality:

1. **Assume** $\overline{M} \subsetneq X$.
2. **Hahn-Banach** produces a nonzero functional $F \in X^*$ vanishing on $M$.
3. A **representation theorem** identifies $F$ concretely (here, as a measure
   via Riesz-Markov).
4. Problem-specific information (here, the discriminatory property) forces
   $F = 0$, a contradiction.

This is a general-purpose machine: the same scheme proves density of test
functions in $L^p$, completeness of orthonormal systems, and many other
approximation results. Only step 4 changes between applications. The price is
that the proof is non-constructive and tells us nothing about rates of
convergence, but when a direct construction is unavailable, the duality approach
is often the only way in.
