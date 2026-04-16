---
kernelspec:
  name: python3
  display_name: Python 3
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/sobolev-duality.pdf
    id: distributions-sobolev-duality-pdf
downloads:
  - id: distributions-sobolev-duality-pdf
    title: Download PDF
---

# Sobolev Duality and Structure

## Duality, reflexivity, and the Sobolev scale

One of the main rewards of working with Sobolev spaces instead of the full
distributional framework is that Sobolev spaces are **Banach spaces**,
and for $1 < p < \infty$, they are **reflexive**. This means that the
entire duality machinery from the duality chapter (weak topology, weak-$*$
topology, Banach–Alaoglu, weak compactness) applies directly, with no need
for the inductive limit subtleties of $\mathcal{D}'(\Omega)$.

### The dual of $W_0^{k,p}(\Omega)$

```{prf:definition} $W_0^{k,p}(\Omega)$ and negative Sobolev spaces
:label: def-sobolev-zero-negative

Let $W_0^{k,p}(\Omega)$ denote the **closure of $C_c^\infty(\Omega)$** in
$W^{k,p}(\Omega)$. For $1 < p < \infty$ with conjugate exponent $p' =
p/(p-1)$, the **negative Sobolev space** is defined as the dual:

$$W^{-k,p'}(\Omega) := \big(W_0^{k,p}(\Omega)\big)^*.$$
```

The duality pairing extends the distributional pairing: for $T \in
W^{-k,p'}(\Omega)$ and $\varphi \in C_c^\infty(\Omega) \subset
W_0^{k,p}(\Omega)$,

$$\langle T, \varphi \rangle_{W^{-k,p'} \times W_0^{k,p}} = \langle T, \varphi \rangle_{\mathcal{D}' \times \mathcal{D}}.$$

So every element of $W^{-k,p'}$ is a distribution, but a tame one: it
extends continuously from test functions to all of $W_0^{k,p}$.

```{prf:remark}
:label: remark-w0-vs-w
:class: dropdown

The distinction between $W_0^{k,p}(\Omega)$ and $W^{k,p}(\Omega)$ matters
on bounded domains: $W_0^{k,p}$ encodes zero boundary conditions (it is
the closure of compactly supported functions), while $W^{k,p}$ does not.
On $\mathbb{R}^d$, they coincide: $W_0^{k,p}(\mathbb{R}^d) =
W^{k,p}(\mathbb{R}^d)$ because $C_c^\infty$ is dense in $W^{k,p}$
on the whole space.
```

### Concrete characterization

The dual characterization makes negative Sobolev spaces concrete. An
element $T \in W^{-k,p'}(\Omega)$ can always be written as

$$\langle T, u \rangle = \sum_{|\alpha| \leq k} \int_\Omega f_\alpha \, D^\alpha u \, dx$$

for some $f_\alpha \in L^{p'}(\Omega)$. Conversely, every such expression
defines an element of $W^{-k,p'}$. In other words:

$$W^{-k,p'}(\Omega) = \left\{ \sum_{|\alpha| \leq k} D^\alpha f_\alpha : f_\alpha \in L^{p'}(\Omega) \right\}$$

where the derivatives are taken in the distributional sense. This is a
representation theorem analogous to the Riesz representation
({prf:ref}`riesz-representation`): every continuous linear functional on
$W_0^{k,p}$ comes from $L^{p'}$ data, with the pairing mediated by
distributional derivatives.

### The Sobolev scale

Sobolev spaces fit into the distributional framework as a graded scale of
increasingly regular subspaces of $\mathcal{D}'(\Omega)$:

$$\cdots \subset H^{-2}(\Omega) \subset H^{-1}(\Omega) \subset L^2(\Omega) \subset H^1(\Omega) \subset H^2(\Omega) \subset \cdots$$

The index $s$ measures regularity: positive $s$ means the function has $s$
derivatives in $L^2$; negative $s$ means the distribution is "mildly
singular," living $|s|$ levels below $L^2$.

```{prf:example} The Dirac delta in the Sobolev scale
:label: delta-sobolev-scale-ch

The Dirac delta $\delta \in \mathcal{D}'(\mathbb{R}^d)$ is not in $L^p$ for
any $p$, but it belongs to negative Sobolev spaces. In dimension $d$ with
$p = 2$, $\delta \in H^{-s}(\mathbb{R}^d)$ for $s > d/2$, because the
Sobolev embedding theorem guarantees that pointwise evaluation is bounded
on $H^s$ when $s > d/2$:

$$|\langle \delta, \varphi \rangle| = |\varphi(0)| \leq C \|\varphi\|_{H^s}.$$

In one dimension, $\delta \in H^{-s}(\mathbb{R})$ for $s > 1/2$. In three
dimensions, $\delta \in H^{-s}(\mathbb{R}^3)$ for $s > 3/2$. The more
singular the object, the further down the scale it lives.
```

```{prf:example} Derivatives shift the scale
:label: ex-derivative-shifts-scale

Differentiation moves a distribution down the Sobolev scale: if $u \in
H^s(\Omega)$, then $D^\alpha u \in H^{s - |\alpha|}(\Omega)$. For
instance:

- If $u \in H^1$, then $u' \in L^2 = H^0$.
- If $u \in L^2$, then $u' \in H^{-1}$. The derivative exists as a
  distribution but is not a function.
- The Heaviside function $H \in L^2(0,1)$ has $H' = \delta_{1/2} \in
  H^{-1}(0,1)$.

The Sobolev index precisely tracks how many derivatives a function can
"afford" before leaving $L^2$.
```

### The limits of the Sobolev scale

As $k$ increases, $H^{-k}$ grows larger, containing increasingly singular
distributions. It is natural to ask whether the union exhausts all of
$\mathcal{D}'(\Omega)$.

```{prf:proposition}
:label: prop-sobolev-scale-strict

The inclusion

$$\bigcup_{k=0}^\infty H^{-k}(\Omega) \subsetneq \mathcal{D}'(\Omega)$$

is strict. The Sobolev scale captures exactly the **finite-order**
distributions. Distributions of **infinite order** (where the order of
the continuity estimate grows without bound as the compact set $K$
expands) escape every level of the scale.
```

```{prf:example} A distribution of infinite order
:label: ex-infinite-order

On $\mathbb{R}$, define

$$T = \sum_{n=1}^\infty \delta^{(n)}(x - n).$$

On a compact set containing $x = n$, the term $\delta^{(n)}(x - n)$
requires $k \geq n$ derivatives of the test function. No single $k$
works for all compact sets, so $T \notin H^{-k}(\mathbb{R})$ for any
$k$. But $T \in \mathcal{D}'(\mathbb{R})$: for any test function
$\varphi$ (which has compact support), only finitely many terms in the
sum are nonzero, so $\langle T, \varphi \rangle$ is well-defined.
```

This is the precise sense in which $\mathcal{D}'(\Omega)$ is larger than
the Sobolev scale: it accommodates distributions whose singularity
**worsens without bound** across the domain. For such objects, the
inductive limit topology of $\mathcal{D}$ is genuinely necessary; no
single Banach space in the scale can hold them.

In practice, distributions arising from PDE theory almost always have
finite order (often order $\leq 2$), so the Sobolev scale is sufficient
for most applications.

### Reflexivity: weak and weak-$*$ for free

```{prf:theorem} Reflexivity of Sobolev spaces
:label: thm-sobolev-reflexive

For $1 < p < \infty$ and $k \geq 0$, the spaces $W^{k,p}(\Omega)$ and
$W_0^{k,p}(\Omega)$ are **reflexive** Banach spaces. In particular,
$H^k(\Omega) = W^{k,2}(\Omega)$ is a reflexive Hilbert space.

For $p = 1$ or $p = \infty$, the Sobolev spaces are **not** reflexive.
```

````{prf:proof}
:class: dropdown

The map $\Phi : W^{k,p}(\Omega) \to \prod_{|\alpha| \leq k}
L^p(\Omega)$ defined by $\Phi(u) = (D^\alpha u)_{|\alpha| \leq k}$ is an
isometric embedding (by definition of the Sobolev norm). The product of
reflexive spaces is reflexive, and $L^p$ is reflexive for $1 < p < \infty$.
A closed subspace of a reflexive space is reflexive, so $W^{k,p}$ is
reflexive.
````

Reflexivity means the canonical embedding $J : W^{k,p} \to (W^{k,p})^{**}$
is surjective, so the double dual adds nothing new. This has immediate
consequences from the duality chapter:

```{prf:corollary} Weak compactness in Sobolev spaces
:label: cor-sobolev-weak-compact

For $1 < p < \infty$:

1. **Banach–Alaoglu applies directly.** The closed unit ball of
   $W^{k,p}(\Omega)$ is weak-$*$ compact in $(W^{-k,p'})^* =
   W^{k,p}$. But because $W^{k,p}$ is reflexive, the weak and weak-$*$
   topologies coincide, so the ball is **weakly compact**.

2. **Every bounded sequence has a weakly convergent subsequence.**
   If $(u_n)$ is bounded in $W^{k,p}(\Omega)$, there exists a subsequence
   $u_{n_j} \rightharpoonup u$ in $W^{k,p}(\Omega)$.

3. **Weak sequential completeness.** Every weakly Cauchy sequence in
   $W^{k,p}(\Omega)$ converges weakly.
```

This is the payoff: in $\mathcal{D}'(\Omega)$, we needed the Montel
property and the non-trivial inductive limit machinery to extract convergent
subsequences. In $W^{k,p}$ for $1 < p < \infty$, it is a direct
consequence of reflexivity and Banach–Alaoglu, results we already proved
in the duality chapter.

```{prf:remark} The duality chapter toolkit, applied
:label: remark-duality-toolkit
:class: dropdown

Here is how the duality chapter results specialize to Sobolev spaces:

| Duality chapter result | Sobolev space consequence |
|---|---|
| Weak topology $\sigma(X, X^*)$ is Hausdorff | Weak limits in $W^{k,p}$ are unique |
| Banach–Alaoglu: unit ball is weak-$*$ compact | Bounded sets in $W^{k,p}$ are weakly precompact ($1 < p < \infty$) |
| Reflexive $\Rightarrow$ weak = weak-$*$ | No need to distinguish weak and weak-$*$ on $W^{k,p}$ |
| Weak convergence + compact operator $\Rightarrow$ strong convergence | $u_n \rightharpoonup u$ in $H^1$ $\Rightarrow$ $u_n \to u$ in $L^2$ (Rellich–Kondrachov) |
| Direct method: minimize over weakly compact sets | Existence of PDE solutions by energy minimization in $H^1$ |

The last row is the reason Sobolev spaces exist: they are the Banach spaces
where the direct method works. Reflexivity gives weak compactness
(subsequences exist), Rellich–Kondrachov gives compact embedding (the
subsequences converge strongly in a weaker norm), and weak lower
semicontinuity of the energy functional closes the argument.
```

### Why $p = 1$ and $p = \infty$ are different

For $p = 1$, the Sobolev space $W^{k,1}(\Omega)$ is not reflexive (just
as $L^1$ is not reflexive). Its dual $(W_0^{k,1})^*$ contains measures
and other singular objects. Bounded sequences in $W^{k,1}$ need not have
weakly convergent subsequences. The direct method fails, and minimization
problems over $W^{1,1}$ require the theory of functions of bounded variation
($BV$) instead.

For $p = \infty$, the space $W^{k,\infty}(\Omega)$ is essentially the
Lipschitz functions (for $k = 1$), and its dual is again non-reflexive.
The weak-$*$ topology on $(W^{k,\infty})^*$ does not coincide with the
weak topology on $W^{k,\infty}$.

The range $1 < p < \infty$ is the sweet spot where duality theory works
cleanly.




