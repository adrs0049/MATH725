# Linear Operators between Banach spaces


```{prf:learning-objectives}
Introduce the Baire category theorem a fundamental tool in the study of linear bounded operators.

1. The Baire category theorem.
2. The Uniform boundedness principle (Banach-Steinhaus).
3. The Open Mapping theorem.
```

---

## The Baire category theorem

In this section we introduce the Baire category theorem. Ultimately the
Baire category theorem is used to answer the question when is a subset $E \subset X$
in a topological space small. This section and in particular the qualiatative and
quantitative discussion is inspired by T. Tao.

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

The next proposition starts to bridge between measure theory and topology. Intuitively
the next proposition shows that sets of positive measure can't be "thinly spread" throughout
space, instead they must be concentrated somewhere in mathematical terms there must be a
ball where the set takes up most of the space.

```{prf:proposition}
Let $E$ be a measurable subset of $\mathbb{R}^d$. Then the following are equivalent
1. $\mu(E) > 0$
2. $\forall \varepsilon > 0$ there exists a ball $B$ such that
   $\mu(E \cap B) \geq (1 - \varepsilon)\mu(B)$
```

```{prf:proof}
:class: dropdown

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
  such that
  $\mu(E \cap B) \geq \frac{1}{2}\mu(B)$

  Since we have $\mu(B) > 0$ we have $\mu(E \cap B) > 0$, and we have that
  $\mu(E) \geq \mu(E \cap B) > 0.$
```

The contrapositive of this statement would be that if a set $E$ never
occupies a large portion of any ball, then $E$ must have measure zero.
In other words, sets of measure zero are nowhere concentrated.

In conclusion, in the measure theoretic perspective the small sets are the nullsets,
and from the topological perspective the small sets are those that are nowhere
dense. The previous discussion gives a "cute" analogy between small sets in a measure
space (i.e. sets that don't occupy a large portion of a ball) and the topological
nowhere dense sets (i.e. not dense in any open ball).

## Baire Category

In this section we want to formalize what it means to be small in a topological space
and start by proving a similar result to the lemma in the previous section.
We begin by giving the small sets a name.

```{prf:definition}
A set $E$ which is not dense in any ball or equivalently a set whose
closure has empty interior is called "meager".
```

```{prf:theorem}
Let $E_1, E_2, \dots$ be an at most countable sequence of subsets of a
complete metric space $X$. If $\bigcup_n E_n$ contains a ball, then
at least one of the $E_n$ is dense in a sub-ball $B'$ of $B$
(and in particular not nowhere dense). To put it in the contrapositive:
the countable union of nowhere dense sets cannot contain a ball.
```

_Why do we care?_ The consequence of this theorem is that
$\mathbb{R}^d$ or $\mathbb{C}^d$ cannot be covered by a countable union of
proper subspaces.

```{prf:definition}
$W \subset V$ is a proper subspace of $V$ such that
1. A subset $V$ i.e. $W \subset V$.
2. Strictly smaller than $V$.
3. Still a vector space.
```

```{prf:example}
In $\mathbb{R}^3$ examples of proper subspaces are:
1. The $xy$-plane.
2. A line through the origin.
3. The origin $\{ (0, 0, 0) \}$.

Baire says that we can't write $\mathbb{R}^3$ as a countable union of these
nowhere dense proper subspaces.
```

```{figure} img/r2_subspaces.svg
:width: 500px
:name: r2-subspaces-fig

$\mathbb{R}^2$ cannot be covered by a countable union of proper subspaces (lines through the origin).

```{prf:remark}
Note that of course we could also prove these results using measure theory
in finite dimensional spaces by using countable additivity of countable unions.
The _advantage_ of Baire's theorem is that it easily extends
to infinite dimensional vectorspaces.
```

### Consequences of the Baire Category theorem

The Baire category theorem leads to three fundamental equivalences between the
qualitative theory of continuous linear operators on Banach spaces e.g.
finiteness, subjectivity to the quantitative theory e.g. estimates.
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


## The uniform boundedness principle (Banach-Steinhaus)


## The Open Mapping Theorem


