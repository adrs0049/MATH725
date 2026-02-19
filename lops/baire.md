# The Baire Category Theorem

In this section we introduce the Baire category theorem. Ultimately the
Baire category theorem is used to answer the question when is a subset $E \subset X$
in a topological space small, which turns out to be a fundamental tools in the study
of linear bounded operators.
This section and in particular the qualiatative and
quantitative discussion is inspired by T. Tao {cite}`tao2009`.

## Small sets in a Measure Space

In a measure theory setting i.e. $X = (X, \mathcal{F}, \mu)$ the "small"
sets are the nullsets i.e. $E \subset X$ such that $\mu(E) = 0$ or subsets
of nullsets. Countable additivity implies that countable unions of nullsets
are of measure zero. This gives us results like this:

```{prf:lemma}
Let $E_1, E_2, \dots$ be an at most countable sequence of measurable sets of
a measure $X$. If
$\mu\left( \bigcup_n E_n \right) > 0$
then at least one of the $E_n$ has positive measure.
```

The next proposition bridges between measure theory and topology. To motivate it, recall that the Lebesgue differentiation theorem tells us that for almost every point $x \in E$, the *density* of $E$ at $x$,

$$\lim_{r \to 0} \frac{\mu(E \cap B(x,r))}{\mu(B(x,r))} = 1,$$

equals one. Such points are called *density points* of $E$ — points where $E$ fills up nearly all of every sufficiently small ball. One can think of density points as measure-theoretic interior points: an interior point of $E$ is one where $E$ contains an entire ball, while a density point is one where $E$ nearly fills every small ball, even if it doesn't contain one outright. The next proposition globalizes this local statement: if $E$ has positive measure, then $E$ must be *dense in some ball* in the measure-theoretic sense that it occupies an arbitrarily large fraction of that ball's volume.

````{prf:proposition}
:label: thm-measure-topo

Let $E$ be a measurable subset of $\mathbb{R}^d$. Then the following are equivalent
1. $\mu(E) > 0$
2. $\forall \varepsilon > 0$ there exists a ball $B$ such that
   $\mu(E \cap B) \geq (1 - \varepsilon)\mu(B)$

```{dropdown} **Proof:**
We prove {prf:ref}`thm-measure-topo` in two steps.
- $(1) \implies (2)$. We proceed by contradiction. Suppose that
    $\mu(E) > 0$ but there exists $\varepsilon_0 > 0$ such that every ball
    satisfies
    $\mu(E \cap B) < (1 - \varepsilon_0) \mu(B)$

    The Lebesgue differentiation theorem implies that for almost every $x\in E$
    we have that
    $\lim_{r \to 0} \frac{\mu(E \cap B(x, r))}{\mu(B(x, r))} = 1$

    Since $E$ has positive measure there must be at least one point where
    the Lebesgue differentiation theorem applies. For this we can find a sufficiently
    small $r$ so that
    $\frac{\mu(E \cap B(x, r))}{\mu(B(x, r))} > 1 - \varepsilon_0.$

    A contradiction.

- $(2) \implies (1)$. Let $\varepsilon = 1/2$, then there exists a ball $B$
    such that $\mu(E \cap B) \geq \frac{1}{2}\mu(B)$

    Since we have $\mu(B) > 0$ we have $\mu(E \cap B) > 0$, and we have that
    $\mu(E) \geq \mu(E \cap B) > 0.$
```
````

Reading the equivalence from both sides:

- **(Forward):** If $\mu(E) > 0$, then $E$ is measure-theoretically dense in some ball — it nearly fills that ball.
- **(Reverse):** If $E$ is not measure-theoretically dense in any ball — that is, in every ball, $E$ always fails to fill a definite fraction — then $\mu(E) = 0$.

A set of measure zero is therefore *nowhere dense in the measure-theoretic sense*: it is never concentrated in any ball. This suggests that to formalize "smallness" in a purely topological setting, we should look for the topological analogue of this property.

## Small Sets in Topological Spaces

To make the analogy with the measure-theoretic setting precise, we first recall what *dense* means in a topological space.

```{prf:definition} Dense in an open set
:label: def-dense-open-set

A set $E$ in a topological space is *dense in an open set $U$* if every nonempty open subset of $U$ intersects $E$, or equivalently, if the closure of $E$ contains $U$.
```

```{prf:remark}
:class: dropdown

Compare this with the measure-theoretic notion from the previous section: there, $E$ is "dense in $B$" if $\mu(E \cap B) \approx \mu(B)$, i.e. $E$ fills almost all the volume of $B$. Here, $E$ is dense in $B$ if $E$ meets every open subset of $B$, i.e. $E$ is topologically everywhere in $B$. Volume has been replaced by topology, but the intuition is the same: $E$ is thoroughly present throughout $B$, with no region where $E$ is absent.
```

```{prf:definition} Nowhere dense
:label: def-nowhere-dense

A set $E$ is *nowhere dense* if it is not dense in any ball, or equivalently, if its closure has empty interior.
```

This is the topological counterpart of a measure-zero set: just as a null set is never measure-theoretically dense in any ball (it never fills a large fraction of any ball), a nowhere dense set is never topologically dense in any ball (its closure contains no open set).

```{prf:theorem} Baire Category Theorem
:label: baire

Let $E_1, E_2, \dots$ be an at most countable sequence of subsets of a
complete metric space $X$. If $\bigcup_n E_n$ contains a ball $B$, then
at least one of the $E_n$ is dense in a sub-ball $B' \subset B$
(and in particular not nowhere dense). To put it in the contrapositive:
the countable union of nowhere dense sets cannot contain a ball.
```

Note that completeness is essential: on an incomplete metric space, the Baire property can fail, and the space itself may be a countable union of nowhere dense sets. This is why completeness is such an important hypothesis throughout the theory of bounded operators. For a proof, see {cite}`hillen2023`.

```{prf:corollary} A complete metric space is not meagre
:label: baire-corollary

Let $X$ be a complete metric space and $\{F_j\}$ a countable collection of nowhere dense sets. Then $\bigcup_{j} F_j \neq X$. Equivalently, a complete metric space is not meagre (i.e. not a countable union of nowhere dense sets).
```

```{prf:example} The rationals are meagre
:label: ex-rationals-meagre

On $X = \mathbb{R}$ (which is complete), the rationals $\mathbb{Q} = \bigcup_{q \in \mathbb{Q}} \{q\}$ are a countable union of nowhere dense sets, hence meagre. {prf:ref}`baire-corollary` tells us $\mathbb{Q} \neq \mathbb{R}$, which we know. More importantly: the irrationals $\mathbb{R} \setminus \mathbb{Q}$ are a dense $G_\delta$ set (a countable intersection of open dense sets), and $\mathbb{Q}$ cannot be $G_\delta$.
```

````{prf:example} **Why do we care?**
:class: dropdown

The consequence of this theorem is that
$\mathbb{R}^d$ or $\mathbb{C}^d$ cannot be covered by a countable union of
proper subspaces.

```{prf:definition} Proper subspaces
:class: dropdown

$W \subset V$ is a proper subspace of $V$ such that
1. A subset $V$ i.e. $W \subset V$.
2. Strictly smaller than $V$.
3. Still a vector space.
```

In $\mathbb{R}^3$ examples of proper subspaces are:
1. The $xy$-plane.
2. A line through the origin.

Baire says that we can't write $\mathbb{R}^3$ as a countable union of these
nowhere dense proper subspaces.

```{figure} /_static/img/r2_subspaces.svg
:width: 500px
:name: r2-subspaces-fig

$\mathbb{R}^2$ cannot be covered by a countable union of proper subspaces (lines through the origin).
```
````

```{prf:remark}
Note that of course we could also prove these results using measure theory
in finite dimensional spaces by using countable additivity of countable unions.
The _advantage_ of Baire's theorem is that it easily extends
to infinite dimensional vectorspaces.
```


```{prf:remark}
:class: dropdown

The Baire Category Theorem holds in two important classes of topological spaces:

1. **Complete metric spaces** (and hence Banach spaces, Hilbert spaces, etc.).
2. **Locally compact Hausdorff spaces** (and hence $\mathbb{R}^d$, $\mathbb{C}^d$, and all finite-dimensional normed spaces).

In finite dimensions these overlap: $\mathbb{R}^d$ is both complete and locally compact. In infinite dimensions, however, a Banach space is *never* locally compact (the closed unit ball is not compact), so completeness is the only route to the Baire property.
```

## Consequences of the Baire Category Theorem

The Baire Category Theorem leads to three fundamental equivalences between the
qualitative theory of continuous linear operators on Banach spaces e.g.
finiteness, surjectivity to the quantitative theory e.g. estimates {cite}`tao2009`.
We have already seen the first of these relationships.
Recall that for a linear operator $A : X \mapsto Y$ we have that
$A\ \mathrm{is\ continuous} \iff\ A\ \mathrm{is\ bounded}.$

As we saw with the examples this allows us to prove the continuity of an operator
$A$ by simply establishing that it is bounded (which usually is easier).

1. _Uniform boundedness principle_ that equates the qualitative
   operators with their quantitative boundedness.

2. _Open mapping theorem_ equates qualitative solvability
   of a linear problem $Lu = f$ with quantitative solvability.

3. _Closed graph theorem_ equates the qualitative regularity
   of a (weakly continuous) operator $T$ with the quantitative regularity of
   the operator.


```{prf:remark}

Note that these results are not used much in practice, because one usually
works in the reverse direction i.e. first prove bounds, and then derive
the operator's qualitative properties. But crucially these results
provide the motivation or justification of why we approach qualitative
problems in functional analysis via their quantitative counter parts.
```

Next we will explore the uniform boundedness principle, and the open
mapping theorem while we leave the closed graph theorem for later.






