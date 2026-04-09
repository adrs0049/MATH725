---
kernelspec:
  name: python3
  display_name: Python 3
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/introduction.pdf
    id: distributions-introduction-pdf
downloads:
  - id: distributions-introduction-pdf
    title: Download PDF
---

# Introduction to Distribution Theory

:::{tip} Big Idea
Distributions are the **dual space** of smooth, compactly supported test
functions. The topology on test functions is *not* a norm topology — it is an
inductive limit of Fréchet spaces. But the topology on distributions
themselves is the **weak-$*$ topology** from the duality chapter,
making convergence of distributions exactly the pointwise convergence of
functionals we have already studied.
:::

## Why distributions?

Classical analysis works with functions that assign values to points. This
breaks down in at least three ways.

**Differentiation destroys regularity.** The absolute value function $|x|$
is continuous but not differentiable at the origin. Its "derivative" should
be the sign function, and the "derivative" of the sign function should be
$2\delta_0$ — but neither of these operations makes sense in the classical
framework. More dramatically, solutions to the wave equation develop shock
discontinuities, and the fundamental solution of Laplace's equation has a
point singularity. We need a derivative that always exists.

**Point evaluation is too rigid.** The Dirac delta "function"
$\delta(x)$, which physicists write as $\int \delta(x) \varphi(x)\, dx =
\varphi(0)$, is not a function — no locally integrable function can
reproduce point evaluation via integration. Yet $\delta$ appears naturally
as the identity for convolution, the fundamental solution of the identity
operator, and the density of a point mass. We need a framework where
$\delta$ is a legitimate object.

**Measures are not enough.** The dual of $C_c(\mathbb{R}^d)$ (continuous,
compactly supported functions) is the space of Radon measures, by the Riesz
representation theorem. Measures handle $\delta$ just fine — it is a point
mass. But the derivative $\delta'$, defined by $\langle \delta', \varphi
\rangle = -\varphi'(0)$, is *not* a measure. It is a genuinely new
object that only exists when the test functions are differentiable. To get a
framework closed under differentiation, we must test against
$C_c^\infty$ rather than just $C_c$.

Distribution theory resolves all three issues in one stroke: define a
**distribution** to be a continuous linear functional on
$\mathcal{D}(\Omega) = C_c^\infty(\Omega)$. Every locally integrable
function, every Radon measure, and every derivative of every distribution is
again a distribution. The price is that we must carefully topologize
$\mathcal{D}(\Omega)$.

## The two topologies

The word "continuous" in the definition of a distribution requires a
topology on $\mathcal{D}(\Omega)$. The right topology turns out to be
surprisingly subtle — no single norm can capture both "all derivatives
converge uniformly" and "supports stay bounded." The solution is an
**inductive limit**: we decompose $\mathcal{D}(\Omega)$ into Fréchet
spaces $\mathcal{D}_K$ (one for each compact $K \subset \Omega$), each
equipped with the seminorms $\|\cdot\|_{C^k(K)}$, and take the finest
locally convex topology making every inclusion continuous. The resulting
convergence is very strong: a sequence $\varphi_n \to \varphi$ only if all
supports sit in a single compact set and all derivatives converge uniformly.
The details of this construction are in the next section.

Once we have $\mathcal{D}(\Omega)$ topologized, its dual
$\mathcal{D}'(\Omega)$ carries the **weak-$*$ topology** — exactly the
construction from the duality chapter. Convergence
$T_n \to T$ in $\mathcal{D}'(\Omega)$ means $\langle T_n, \varphi \rangle
\to \langle T, \varphi \rangle$ for every test function $\varphi$. This is
**convergence in the sense of distributions**, one of the weakest
convergence notions in analysis, yet limits are unique (the weak-$*$
topology is Hausdorff) and every Cauchy sequence converges.

## The hierarchy of generalized functions

Distribution theory fits into a chain of increasing generality:

$$
C^\infty(\Omega) \subset C(\Omega) \subset L^1_{\mathrm{loc}}(\Omega)
\subset \mathcal{M}(\Omega) \subset \mathcal{D}'(\Omega)
$$

where $\mathcal{M}(\Omega)$ denotes Radon measures. Each inclusion is
strict:

- The sign function is in $L^1_{\mathrm{loc}}$ but not continuous.
- The Dirac delta $\delta$ is a measure but not in $L^1_{\mathrm{loc}}$.
- The derivative $\delta'$ is a distribution but not a measure.

The embedding $L^1_{\mathrm{loc}}(\Omega) \hookrightarrow
\mathcal{D}'(\Omega)$ given by $f \mapsto T_f$, where $\langle T_f,
\varphi \rangle = \int f \varphi\, dx$, is injective and continuous. This
justifies identifying a function with the distribution it defines — we
write $\langle f, \varphi \rangle$ instead of $\langle T_f, \varphi \rangle$
without ambiguity.

## What comes next

With the overview in hand, we now develop the details:

1. **Test functions and their topology** — the inductive limit
   construction, sequential convergence, and key properties of
   $\mathcal{D}(\Omega)$.

2. **Distributions as continuous linear functionals** — the formal
   definition, the weak-$*$ topology, separation properties, and the
   fundamental examples.

3. **Operations on distributions** — differentiation, multiplication
   by smooth functions, and convolution, all defined by duality.

4. **Sobolev spaces** $W^{k,p}(\Omega)$ — where distributional
   derivatives meet $L^p$ integrability, giving Banach spaces suited
   to PDE theory.


## References

```{bibliography}
:filter: docname in docnames
```
