# The Open Mapping Theorem

The open-mapping theorem is another of the big theorems of functional analysis. Its signifiance is that
it equates qualitative properties solvability of a linear problem $Lx = y$ with quantitative solvability.
We will begin by stating the qualitative version and explore its consequences on the solvability of
linear operators, followed by the quantitative version.

```{prf:theorem} Open Mapping Theorem
Let $U, V$ be the open units balls of the Banach spaces $X, Y$ respectively. To every bounded linear
operator $L$ of $X$ **onto** $Y$ there corresponds $\delta > 0$ so that
$L(U) \subset \delta V = \{ y \in Y : ||y|| < \delta \}.$
```

By the linearity of $L$ we see that this theorem says that $L$ maps open sets to open sets i.e. is an
open mapping, and that for every $||y|| < \delta$ there corresponds on $x$ such that $||x|| < 1$ so that
$Lx = y$.

````{prf:corollary} Banach's Bounded Inverse Theorem

Let $L$ be a linear operator between two Banach spaces $X$ and $Y$, that is **onto** and one-to-one, then
$L^{-1}$ is a bounded linear operator.

```{dropdown} **Proof:**

If $||Lx|| < \delta$ then the open mapping theorem says that $Lx \in L(U)$ thus there
exists a $u \in U$ such that $Lu = Lx$. The **key** is that since $L$ is injective we have $x = u$,
so that we conclude that $||x|| < 1$. If $||x|| \geq 1$ then $||Lx||\geq \delta$. Now let
$y := \frac{x}{||x||}$ then $||Ly|| \geq \delta$ so that we have $||Lx|| \geq \delta ||x||$.
Now define $L^{-1}$ via $L^{-1} y= x$ if $Lx = y$. We then show that $L^{-1}$ is indeed linear,
and bounded $||L^{-1}|| \leq 1/\delta$.

```
````

```{prf:remark}
The previous statement is remarkable in the sense that it lifts our intuition about linear opeartors
in finite dimensions (i.e. that bijectiveness is equivalent to invertibility) to the infinite dimensional
case.
```

Now to the version of the open-mapping theorem by T. Tao.

````{prf:theorem}
Let $L : X \mapsto Y$ be a bounded linear operator between two Banach spaces, then the following
are equivalent:

1. $L$ is onto.
2. $L$ is open.
3. (Qualitative solvability). For every $y \in Y$ there exists (*not necessarily unique*) a solution
$x \in X$ to the equation $Lx = y$.
4. (Quantitative solvability). $\exists C > 0 : \forall y \in Y,\ \exists x \in X$ to $Lx = y$ such that
$|| x || \leq C || y ||$.
5. (Quantitative solvability for dense subsets). There exists a $C > 0$ such that for a dense set of $y$ in $Y$
there exists solutions $x \in X$ to $Lx = y$ which obeys $||x|| \leq C || y ||$.


```{dropdown} **Proof:**
Todo. Finish.

```
````

