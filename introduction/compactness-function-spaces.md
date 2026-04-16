---
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/compactness-function-spaces.pdf
    id: introduction-compactness-function-spaces-pdf
downloads:
  - id: introduction-compactness-function-spaces-pdf
    title: Download PDF
---

# Compactness in Function Spaces

In infinite dimensions, "bounded" does not imply "precompact"
({prf:ref}`ex-unit-ball-l2-not-compact`). To pin down compactness in the two
function spaces we care about ($C(K)$ and $L^p$) we need additional
structure. Two classical theorems give the right structure: Arzelà-Ascoli
for continuous functions, and its $L^p$ analog Kolmogorov-Riesz for
integrable functions. Both will be cited repeatedly throughout the course.

## Arzelà-Ascoli for $C(K)$

```{prf:theorem} Arzelà-Ascoli
:label: thm-arzela-ascoli

Let $K$ be a compact metric space and $\mathcal{F} \subset C(K)$ a family of
continuous functions. Then $\mathcal{F}$ is precompact (in the sup norm) if
and only if

1. **(pointwise bounded)** $\sup_{f \in \mathcal{F}} |f(x)| < \infty$ for
   every $x \in K$,
2. **(equicontinuous)** for every $\varepsilon > 0$ there exists $\delta > 0$
   such that $|f(x) - f(y)| < \varepsilon$ whenever $d(x, y) < \delta$, for
   all $f \in \mathcal{F}$ simultaneously.
```

The two conditions prevent the two ways a sequence of continuous functions
can fail to have a uniformly convergent subsequence: the values cannot blow
up (boundedness), and they cannot oscillate arbitrarily fast (equicontinuity).
A typical use: bounded sequences of $C^1$ functions on a compact interval
are equicontinuous because $|f(x) - f(y)| \leq \|f'\|_\infty |x - y|$, hence
precompact in $C^0$ by Arzelà-Ascoli.

## Kolmogorov-Riesz for $L^p$

The same question arises one floor down. Nesting ({prf:ref}`rem-rainbow`)
tells us $L^p(\Omega) \subset L^q(\Omega)$ continuously when
$p \geq q$ and $|\Omega| < \infty$. Is this embedding *compact*?

The answer is **no**. On $\Omega = (0, 2\pi)$, the sequence
$u_n(x) = \sin(nx)$ has $\|u_n\|_{L^p} \leq C$ for every $p \in [1, \infty]$,
so it is bounded in every $L^p$. Yet any two distinct terms satisfy
$\|u_n - u_m\|_{L^q} \not\to 0$: the sequence has no convergent
subsequence in $L^q$, for any $q$. Integrability alone does not suppress
oscillation.

The $L^p$ analog of Arzelà-Ascoli gives a complete answer.

```{prf:theorem} Kolmogorov-Riesz-Fréchet
:label: thm-kolmogorov-riesz

Let $1 \leq p < \infty$. A bounded set $K \subset L^p(\mathbb{R}^d)$ is
precompact if and only if

1. **(bounded)** $\sup_{u \in K} \|u\|_{L^p} < \infty$,
2. **(equicontinuous under translation)** $\sup_{u \in K} \|\tau_h u - u\|_{L^p} \to 0$ as $h \to 0$, where $\tau_h u(x) = u(x - h)$,
3. **(tight)** $\sup_{u \in K} \|u\|_{L^p(|x| > R)} \to 0$ as $R \to \infty$.

On a bounded domain $\Omega$, condition (3) is automatic, so precompactness
reduces to (1) and (2).
```

Each condition prevents a specific way mass can escape:
- (1) prevents mass from blowing up in size,
- (2) prevents mass from escaping into high frequencies, since a function
  whose translations converge uniformly cannot oscillate arbitrarily fast,
- (3) prevents mass from escaping to spatial infinity.

This is the $L^p$ mirror of Arzelà-Ascoli: "bounded + equicontinuous + stays
in a compact set" gives precompactness, with $L^p$-equicontinuity-under-
translation playing the role of pointwise equicontinuity.

In later chapters, this theorem is the structural reason Sobolev embeddings
produce compactness. A gradient bound of the form $\|\nabla u\|_{L^p} \leq M$
supplies condition (2) automatically: by the fundamental theorem of
calculus, $\|\tau_h u - u\|_{L^p} \leq |h|\,\|\nabla u\|_{L^p}$. So *the
Rellich-Kondrachov theorem is Kolmogorov-Riesz applied to the Sobolev ball*,
with the equicontinuity condition upgraded from a hypothesis to a consequence
of gradient control.
