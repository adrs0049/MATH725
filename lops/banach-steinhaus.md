---
exports:
  - format: pdf
    template: plain_latex
    output: exports/banach-steinhaus.pdf
    id: lops-banach-steinhaus-pdf
downloads:
  - id: lops-banach-steinhaus-pdf
    title: Download PDF
---

# The uniform boundedness principle (Banach-Steinhaus)



```{prf:theorem} Banach-Steinhaus
:label: banach-steinhaus

Let $X$ be a Banach space, and $Y$ be a normed space and let $(T_\alpha)_{\alpha \in A}$ be a family
of bounded linear operators $T_\alpha : X \mapsto Y$. Then the following are equivalent:

1. (Pointwise boundedness) $\forall x \in X$ the set $\{ T_\alpha x : \alpha \in A \}$ is bounded.
2. (Uniform boundedness) The operator norms $\{ || T_\alpha ||_{\mathrm{op}} \} $ are bounded.

```

```{dropdown} **Proof** of Banach-Steinhaus:

The hard direction is (1) $\implies$ (2). The key strategy of the proof is to invoke the Baire category
theorem {prf:ref}`baire`. We invoke the theorem by constructing a covering for the complete space $X$.
In detail, define the following subsets of $X$:

$$ E_j = \{ x \in X : || T_{\alpha} x ||_Y \leq j\ \forall \alpha \in A \} $$

Since by assumption we have that $\sup_{\alpha \in A} || T_\alpha x || < \infty$ this implies that
the $E_j$ indeed cover $X$ i.e.

$$ \bigcup_{j=1}^{\infty} E_j = X $$

Since $X$ is complete, {prf:ref}`baire` says that at least one of the $E_j$ is not nowhere dense i.e.
has non-empty interior. Let's denote that set by $E_n$. Then there exists
$B_r(y) \subset E_n$. Let $z \in B_r(y)$, then $z \in E_n$ and $||y - z|| < r$ and we can write
$z = y + x = y + (z - y)$ then we have $||x|| < r$, and $y + x \in E_n$.

$$ || T_{\alpha} x || = || T_{\alpha}(x + y) - T_{\alpha} y || \leq n + || T_{\alpha} y || \leq R $$

for some $R > 0$. In particular, for $||x|| = r$ we have

$$ ||T_{\alpha} x|| \leq R \frac{||x||}{r},\ \forall \alpha \in A $$

Since for arbitrary $x \in X$ we can consider $\tilde{x} = r \frac{x}{||x||}$ with $||\tilde{x}|| = r$
and we have

$$
    || T_{\alpha} x || = || (T_{\alpha} \tilde{x})(\frac{||x||}{r}) ||
                       = \frac{||x||}{r} || T_{\alpha} \tilde{x} ||
                    \leq \frac{||x||}{r} \frac{R}{r} ||\tilde{x} || = \frac{R}{r} || x ||
$$

All that remains now is to compute the operator norm from its definition, to find that

$$ || T_{\alpha} ||_{\mathrm{op}} := \sup_{x \neq 0} \frac{|| T_{\alpha} x ||}{||x||} \leq \frac{R}{r}. $$

```

```{prf:remark} Significance of Banach-Steinhaus
:label: rem-bs-significance

1. The condition that $\{ \| T_\alpha \| : \alpha \in A \}$ is bounded is equivalent to the family
$\{ T_\alpha \}$ being equicontinuous.

2. The theorem shows that pointwise control implies uniform control.

3. From the perspective of qualitative vs. quantitative: the qualitative statement says
the family of operators is somehow well-behaved, and the quantitative perspective puts a
particular number on the behaviour of the operator.

4. A version of this theorem with specific rates allows us to establish and control the convergence
of sequences of approximation operators e.g. quadrature approximations to integrals, or finite
difference approximations to derivatives.

5. From a metamathematical view it explains why sequential arguments often work in functional analysis.
In other words, if the uniform limit didn't exist we could construct sequences that behave pathologically.
For more details, see the subsequent corollary.
```

## Why Does Banach-Steinhaus Need Completeness?

In finite dimensions, Banach-Steinhaus is trivial: it needs no topology, no Baire, not even
continuity. In infinite dimensions completeness is essential.

::::{dropdown} **The Finite-Dimensional Story**

Let $\{T_\alpha\}$ be a family of linear maps $\mathbb{R}^n \to Y$, pointwise bounded. Pick a basis
$e_1, \dots, e_n$. Pointwise boundedness gives finite constants
$M_i = \sup_\alpha \|T_\alpha e_i\| < \infty$ for each $i$. For any $x = \sum c_i e_i$ with
$\|x\| \leq 1$, equivalence of norms gives $|c_i| \leq C$ for some universal constant, so:

$$
\|T_\alpha x\| \leq \sum_{i=1}^{n} |c_i| \, \|T_\alpha e_i\| \leq C \sum_{i=1}^{n} M_i.
$$

Done. $\sup_\alpha \|T_\alpha\| \leq C(M_1 + \cdots + M_n)$. The argument is just the triangle
inequality applied to **finitely many** basis vectors. Pointwise boundedness on $n$ basis vectors
immediately gives a uniform bound, because every point is a finite linear combination of them with
controlled coefficients. In infinite dimensions this sum becomes an infinite series, which has no reason
to converge --- the finite-dimensional trick breaks down completely.

::::

::::{dropdown} **What Breaks in Infinite Dimensions**

Let $X = c_{00}$ be the space of real sequences with only finitely many nonzero terms, equipped with the sup-norm $\|x\|_\infty = \max_k |x_k|$.

**Why $c_{00}$ is not complete.** Consider the sequence of elements

$$
x^{(n)} = \left(1, \frac{1}{2}, \frac{1}{3}, \ldots, \frac{1}{n}, 0, 0, \ldots\right) \in c_{00}.
$$

This is Cauchy in the sup-norm: for $m > n$,
$\|x^{(m)} - x^{(n)}\|_\infty = \max_{k=n+1}^{m} \frac{1}{k} = \frac{1}{n+1} \to 0.$
But the limit $x = (1, 1/2, 1/3, \ldots)$ has infinitely many nonzero terms, so $x \notin c_{00}$. The completion of $c_{00}$ in the sup-norm is $c_0$, the space of sequences converging to zero.

**The operators.** Define $T_n : c_{00} \to \mathbb{R}$ by $T_n(x) = n \cdot x_n$. Each $T_n$ is a bounded linear functional with $\|T_n\|_{\mathrm{op}} = n$.

**Pointwise bounded:** For any fixed $x \in c_{00}$, there exists $N$ such that $x_k = 0$ for $k > N$. Then $T_n(x) = n \cdot x_n = 0$ for all $n > N$, so
$\sup_n |T_n(x)| = \max_{1 \leq n \leq N} n|x_n| < \infty.$

**Not uniformly bounded:** But $\|T_n\|_{\mathrm{op}} = n \to \infty$.

So Banach-Steinhaus fails on the incomplete space $c_{00}$: the family is pointwise bounded but uniformly unbounded.

### Where is the witness?

The contrapositive of Banach-Steinhaus promises: if the family is uniformly unbounded, there exists a
single $x$ with $\sup_n n|x_n| = \infty$. Since $\|T_n\|_{\mathrm{op}} = n \to \infty$, Banach-Steinhaus applied on the *complete* space $c_0$ tells us (by contrapositive) there **must** exist an $x \in c_0$ where $\sup_n |T_n(x)| = \infty$. We can find it explicitly: take

$$
x = \left(\frac{1}{\sqrt{1}}, \frac{1}{\sqrt{2}}, \frac{1}{\sqrt{3}}, \ldots\right).
$$

This is in $c_0$ (since $1/\sqrt{n} \to 0$) but not in $c_{00}$. Then
$T_n(x) = n \cdot \frac{1}{\sqrt{n}} = \sqrt{n} \to \infty.$

**But this witness is not in $c_{00}$.** It has infinite support. The witness lives in the completion $c_0$, not in the finitely supported subspace. The incomplete space has a **hole** exactly where it needs to be.

The catastrophe was always there, you just couldn't see it because $c_{00}$ is missing the elements that expose the problem. The incomplete space gives a **false sense of security**: everything you can test looks fine, but the moment someone hands you an input from the completion, it blows up. This is the applied mathematics moral: you build your numerical scheme on finitely supported data (effectively $c_{00}$), your convergence tests all pass, and then in production someone feeds in an input from $c_0$ and the scheme explodes. Completeness isn't an abstraction, it's the guarantee that your test cases are *representative* of the full space.

**What goes wrong with the Baire argument?** We would write $c_{00} = \bigcup_j F_j$ where $F_j = \{x : |T_n(x)| \leq j \text{ for all } n\}$. These $F_j$ do cover $c_{00}$, but since $c_{00}$ is not complete, it is **not a Baire space**. Each $F_j$ is nowhere dense: given any $x \in F_j$ and $\varepsilon > 0$, choose $n > j/\varepsilon$ and perturb the $n$-th coordinate by $\varepsilon/2$ to find a point $y \in B_\varepsilon(x) \setminus F_j$. No $F_j$ contains a ball, so the Baire argument has no traction. Completeness would forbid this: in a Banach space, at least one $F_j$ must have nonempty interior, and linearity propagates that local bound to a global one.

::::

## Why This Matters in Practice

The contrapositive is often more useful: if the family is uniformly unbounded, then there exists a concrete point $x$ where $\sup_\alpha \|T_\alpha x\| = \infty$. The blowup cannot remain invisible, it must concentrate at an actual point in the space. Moreover, the set of such witness points is **comeager** (residual) by Baire, meaning witnesses are generic and the well-behaved points are the topologically rare ones.

::::{dropdown} **Fourier series**

The partial sum operators $S_n : C[0,1] \to C[0,1]$ satisfy $\|S_n\| \to \infty$ (the Lebesgue
constants grow like $\log n$). Banach-Steinhaus immediately gives: there exists a **specific continuous
function** whose Fourier partial sums diverge at a point. Not a pathological distribution, not
something outside $C[0,1]$, but an actual continuous function. This is the du Bois-Reymond theorem (1876),
and the Banach-Steinhaus proof is essentially one line once you know the norms grow. Moreover, such
functions are **generic**: the typical continuous function has a divergent Fourier series.

::::

::::{dropdown} **Numerical methods and approximation**

If an approximation scheme has operator norms growing to infinity, Banach-Steinhaus guarantees a
concrete input where convergence fails, and generically most inputs fail. The Runge phenomenon
(polynomial interpolation blowing up at equispaced nodes) can be understood this way: the
interpolation operators are unbounded, so a witness function exists where interpolation diverges.

The practical message is: if you are designing a numerical scheme and you cannot prove uniform
boundedness of the operator norms, you should not think "maybe it works for the inputs I care about."
Banach-Steinhaus says the failure is not hiding in some exotic corner, it is **dense**. You will
encounter it.

::::

Banach-Steinhaus turns abstract collective pathology into concrete individual pathology. An incomplete space is itself meagre, so it can be exhausted by the nowhere dense sets $F_j$ and no witness needs to exist. A complete space is not meagre, so Baire forces some $F_j$ to have interior, and the witness is not only guaranteed but *generic*.

A common application is to converging sequences of bounded linear operators.

````{prf:corollary} Limits of sequences of bounded linear operators

Let $X, Y$ be Banach spaces, and let $( T_n )_{n=1}^{\infty}$ be a family of
bounded linear operators $T_n : X \mapsto Y$. Then the following are equivalent:

1. (Pointwise convergence). $\forall x \in X$, $T_n x \to y$ in $Y$.
2. (Pointwise convergence to a continuous limit). There exists a bounded linear operator $T : X \mapsto Y$
such that $\forall x \in X$, $T_n x \to Tx$ in $Y$.
3. (Uniform boundedness + Dense subclass convergence). The operator norms $\{ ||T_n|| : n = 1, 2, \dots \}$
are bounded, and for a dense subset of $X$, $T_n x$ converges in $Y$.

```{dropdown} **Proof:**
Homework.
```
````


