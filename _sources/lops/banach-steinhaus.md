# The uniform boundedness principle (Banach-Steinhaus)



````{prf:theorem} Banach-Steinhaus

Let $X$ be a Banach space, and $Y$ be a normed space and let $(T_\alpha)_{\alpha \in A}$ be a family
of bounded linear operators $T_\alpha : X \mapsto Y$. Then the following are equivalent:

1. (Pointwise boundedness) $\forall x \in X$ the set $\{ T_\alpha x : \alpha \in A \}$ is bounded.
2. (Uniformed boundedness) The operator norms $\{ || T_\alpha ||_{\mathrm{op}} \} $ are bounded.

```{dropdown} **Proof:**

The hard direction is (1) $\implies (2). The key strategy of the proof is to invoke the Baire category
theorem {prf:baire}. We invoke the theorem by constructing a covering for the complete space $X$.
In detail, define the following subsets of $X$:

$$ E_j = \{ x \in X : || T_{\alpha} x ||_Y \leq j\ \forall \alpha \in A \} $$

Since by assumption we have that$\sup_{\alpha \in A} || T_\alpha x || < \infty$ this implies that
the $E_j$ indeed cover $X$ i.e.

$$ \Bigcup_{j=1}^{\infty} E_j = X $$

Since $X$ is complete, {prf:baire} says that at least one of the $E_j$ is not nowhere dense i.e.
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
````

```{prf:remark}
Why is this theorem so signifiancant?

1. Note that the condition that $\{ || T_\alpha || : \alpha in A \}$ is equivalent to the family
$\{ T_\alpha \}$ to be equicontinuous.

2. The signifiance of this theorem is that it shows that pointwise control implies uniform control.

3. From the perspective of qualitative vs. quantitative we have the qualitative statement
that the family of operators is somehow well-behaved, and the quantitative perspective which puts a
particular number on the behaviour of the operator.

4. A version of this theorem with specific rates allows us to establish and control the convergence
of sequences of approximation operators e.g. quadratures approximations to integrals, or finite
difference approximations to derivatives. As soon as I have time I will add some more details on this
via some worked out examples.

5. From a metamathematical view it explains why sequential arguments often work in functional analysis.
In other words, if the uniform limit didn't exist we could construct sequences that behave pathological.
For more details, see the subsequent corollary.
```

A common application is to converging sequences of bounded linear operators.

````{prf:corollary} Limits of sequences of bounded linear operators

Let $X, Y$ be Banach spaces, and let $( T_n )_{n=1}^{\infty}$ be a family of
bounded linear operators $T_n : X \mapsto Y$. Then the following are equivalent:

1. (Pointwise convergence). $\forall x \in X$, $T_n x \to y$ in $Y$.
2. (Pointwise convergence to a continuous limit). There exists a bounded linear opreator $T : X \mapsto Y$
such that $\forall x \in X$, $T_n x \to Tx$ in $Y$.
3. (Uniform boundedness + Dense subclass convergence). The operator norms $\{ ||T_n|| : n = 1, 2, \dots \}$
are bounded, and for a dense subset of $X$, $T_n x$ converges in $Y$.

```{dropdown} **Proof:**
    Homework.
```


````
