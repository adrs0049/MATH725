# The Hahn-Banach Theorem


```{prf:theorem} Hahn-Banach theorem

Let $X$ be a normed space, let $Y \subset X$ be a subspace. Then any continuous linear functional
$\lambda \in Y^*$ on $Y$ can be extended to a continuous linear functional $\hat{\lambda} \in X^*$
on $X$ with the same operator norm, thus $\hat{\lambda}$ agrees with $\lambda$ on $Y$
and $|| \hat{\lambda}||_{X^*} = ||\lambda||_{Y^*}$.
**Note** that $\hat{\lambda}$ is not necessarily unique.

```


## Geometric Implications

There are three illustrative corollaries of the Hahn-Banach theorem.


```{prf:corollary} The distinguishing property

Let $x, y \in X$. If $f(x) = f(y)$ for all $f \in X^*$ then $x = y$.

```


```{prf:corollary} Norming property

For each $x \in X$ there exists $f \in X^*$ with $f(x) = ||x||$ and $||f||_{op} = 1$.

```


```{prf:corollary} Classification of closures

Let $M$ be a linear subspace of a normed space $X$ and let $x_0 \in X$ then $x_0 \in \overline{M}$
if and only if there exists **no** bounded linear functional $f$ such that $f(x) = 0$ for all $x \in M$
but $f(x_0) \neq 0$.

```
