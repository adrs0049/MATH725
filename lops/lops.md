# Linear Operators on Banach spaces

Linear operators between Banach spaces are key in functional analysis. They connect function spaces
with each other, describe physical systems, cost functions, solve PDEs, and tell us when Banach spaces
are isomorphic.

```{prf:definition} Linear operator

Let $(X, ||\cdot||_X)$ and $(Y, ||\cdot||_Y)$ be two Banach spaces, and let $A : X \mapsto Y$ be a map:

1. $A$ is linear if $A(\alpha x_1 + \beta x_2) = \alpha Ax_1 + \beta Ax_2$.
2. $A$ is bounded if $||Ax||_Y \leq M ||x||_X$ $\forall x \in X$, $M > 0$.
3. We denote the set of all bounded operators by

$$\mathcal{L}(X, Y) = \{ A : X \mapsto Y,\ A\ \mathrm{linear\ and\ bounded} \}$$

This space is equipped with a norm

$$ || A ||_{\mathrm{op}} := \sup_{x \neq 0} \frac{||Ax||_Y}{||x||_X} = \sup_{||x||=1} || Ax ||_Y $$
```

````{prf:proposition} $\mathcal{L}(X, Y)$ is a Banach Space

```{dropdown} **Proof:**

Insert proof.

```
````

````{prf:proposition} Qualitative vs Quantitative properties
Let $A : X \mapsto Y$ be linear, then $A$ is bounded if and only if $A$ is continuous.

```{dropdown} **Proof:**

1. If $A$ is bounded, then let $x_n \to x$ in $X$ then

$$ || Ax_n - Ax || = || A(x_n - x) || \leq ||A||_{\mathrm{op}} || x_n - x || $$

Now let $x_n \to x$ and $A$ must be continuous.

2. If $A$ is continuous, and $A$ is not bounded. Then there exists a sequence $y_n$ in $X$ such that

$$ ||Ay_n||_Y \geq n^2 ||y_n|| \quad\mathrm{and define}\quad x_n := \frac{y_n}{n || y_n ||} \to 0 $$

But $||Ay_n|| \geq n \to \infty$ means that $A$ is not continuous, we found a contradiction that $A$
is not continuous at zero.

```
````

```{prf:remark}

This is the first result of the qualitative vs. quantitative theme we encounter in functional analysis.
With qualitative we here mean that $A$ is continuous i.e. well behaved, and that this is related to a
quantitative bound on the operator which quantifies how well behaved the operator is. In terms of
continuity it tells us how much the output can vary as we change the input.

```


```{prf:example}

Insert example of integral operator.

```

```{prf:example}

Insert example of second order differential operator.

```

```{prf:definition}
Let $A : X \mapsto Y$ we define
1. The **range** of the operator as $R[A] = \{ g \in Y : g = A[f],\ f \in D(A) \}$
2. The **nullspace** or **kernel** of $A$ is $N[A] = \{ f \in D(A) : A[f] = 0 \}$.
```

