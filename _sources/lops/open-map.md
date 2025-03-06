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

```{prf:corollary} Banach's Bounded Inverse Theorem
:label: banach-inverse

Let $L$ be a linear operator between two Banach spaces $X$ and $Y$, that is **onto** and one-to-one, then
$L^{-1}$ is a bounded linear operator.
```

```{dropdown} **Proof** of Banach's Bounded Inverse Theorem:
If $||Lx|| < \delta$ then the open mapping theorem says that $Lx \in L(U)$ thus there
exists a $u \in U$ such that $Lu = Lx$. The **key** is that since $L$ is injective we have $x = u$,
so that we conclude that $||x|| < 1$. If $||x|| \geq 1$ then $||Lx||\geq \delta$. Now let
$y := \frac{x}{||x||}$ then $||Ly|| \geq \delta$ so that we have $||Lx|| \geq \delta ||x||$.
Now define $L^{-1}$ via $L^{-1} y= x$ if $Lx = y$. We then show that $L^{-1}$ is indeed linear,
and bounded $||L^{-1}|| \leq 1/\delta$.
```

```{prf:remark}
The previous statement is remarkable in the sense that it lifts our intuition about linear opeartors
in finite dimensions (i.e. that bijectiveness is equivalent to invertibility) to the infinite dimensional
case.
```

Now to the version of the open-mapping theorem by T. Tao {cite}`tao2009`.

```{prf:theorem} Quantitative and Qualitative version of the Open Mapping Theorem
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
```

```{dropdown} **Proof:**

**(1) $\iff$ (3):** by the definition of surjectiveness.

**(2) $\implies$ (1):** If $L$ is open, then $L(B_X(0, 1))$ is an open set in $Y$ containing $L(0) = 0$. Thus
there exists $r > 0$ such that $B_Y(0, r) \subset L(B_X(0, 1))$. Now pick any $y \in Y$ and any scalar $t > 0$,
we can use the **linearity** of $L$ in the following way, $L(B_X(0, t)) = L(t B_X(0, 1)) = t L(B_X(0, 1))$.

Now since $B_Y(0, r) \subset L(B_X(0, 1))$ we also have that $B_Y(0, tr) = t B_Y(0, r) \subset L(B_X(0, t))$.
Now set $t = 2 ||y|| / r$ then $y \in B_Y(0, 2 ||y||) \subset L(B_X(0, 2 ||y||/r))$, which means that
there exists an $x \in B_X(0, 2||y||/r)$ such that $Lx = y$, further note that we have $||x|| < 2||y|| / r$.

**(2) $\implies$ (4):** If $L$ is open, then $B_Y(0, r) \subset L(B_X(0, 1))$ for some $r > 0$. Pick $y \in Y$
then $\tilde{y} := \frac{y}{||y||}\frac{r}{2} \in B_Y(0, r)$, so there exists $z \in B_X(0, 1)$ such that
$Lz = \tilde{y}$. Define $x = \frac{2||y||}{r} z$, which by **linearity** gives us $Lx = y$. Now since
$||z|| < 1$ we have $||x|| < \frac{2||y||}{r}$. Now define $C := \frac{2}{r}$ and we have $||x|| \leq C ||y||$
for any $y \in Y$.

**(4) $\implies$ (2):** Assume that for every $y\in Y$ there exists $x \in X$ such that $Lx = y$ and $||u||\leq C||y||$.
We begin by showing that $L$ maps the unit ball to an open set. Let $y \in Y$ with $||y|| < \frac{1}{C}$,
then there exists $x \in X$ such that $Lx = y$ and $||x|| < C ||y|| < 1$. This means that $y \in L(B_X(0,1))$.
Thus we have shown that $B_Y(0, \frac{1}{C})\subset L(B_X(0, 1))$, making $L(B_X(0, 1))$ an open set.
By **linearity** of $L$ this means that $L$ maps all open sets to open sets, therefore $L$ is open.

**(4) $\implies$ (5):** If it holds everywhere it will hold for a dense set.

**(5) $\implies$ (4):** Let $E \subset Y$ be the dense set, and let $y \in Y$ then want to approximate
$y$ using elements in $E$.

- **Step 1:** Set the initial **residual** $r_0 = y$, then find $y_1 \in E$ so that
$||y_1 - r_0|| < \varepsilon = \frac{1}{2} ||y||$.

- **Step 2:** Set the second **residual** $r_1 = r_0 - y_1 = y - y_1$, and find $y_2 \in E$ so that

$$
    ||y_2 - r_1|| < \frac{1}{2}||r_1|| < \frac{1}{4}||y||
$$

- **Step 3:** At the $j$-the step we define $r_j = r_{j-1} - y_j$ where $y_j \in E$ with

$$
    ||y_j - r_{j-1}|| < \frac{1}{2} ||r_{j-1}|| < 2^{-j} ||y||
$$

Note that the sequence of residuals has $||r_j|| \to 0$ and thus $r_j \to 0$, and note that
$y_j = r_{j-1} - r_j$ so if we sum the $y_j$s we find a telescoping series i.e.

$$
    \sum_{j=1}^{\infty} y_j = \lim_{N \to \infty} \sum_{j=1}^{N} r_{j-1} - r_j = r_0 - \lim_{N\to\infty} r_N = y.
$$

Finally we show that we can life the inequality from the dense set to everywhere. Since $y_j \in E$ we have
there exists $x_j : Lx_j = y_j$ with $||x_j|| \leq C ||y_j||$. Then

$$
    ||y_j|| = ||y_j + r_{j-1} - r_{j-1}|| \leq 2^{-j} ||y|| + 2^{-(i-1)} ||y|| \leq 4 \cdot 2^{-i} ||y||.
$$

Since $y_j\in E$ we have that

$$
    ||x_j|| \leq C ||y_j|| \leq 4C \cdot 2^{-j} ||y|| \quad\implies\quad \sum_{j=1}^{\infty} ||x_j|| < 4C||y||.
$$

Hence we can define $x:= \sum_{j=1}^{\infty} x_j$. Finally

$$
    Lx = L[\sum_{j=1}^{\infty} x_j] = \sum_{j=1}^{\infty} Lx_j = \sum_{j=1}^{\infty} y_j = y.
$$

Thus we have that $Lx = y$ and similarly find that $||x|| \leq 4C ||y||$.

**(3) $\implies$ (4):** The strategy is to apply the {prf:ref}`baire`. Since by assumption $\forall y \in Y$
there exists $x \in X$ such that $Lx = y$ the following $E_n$ form a cover of $Y$.

$$
    E_n = \{ y \in Y : ||x|| \leq n ||y||\ \mathrm{such\ that}\ Lx = y \}\ \mathrm{and}\ \bigcup_n E_n = Y.
$$

Since $Y$ is complete, Baire's theorem implies that at least one of the $E_n$'s is not nowhere dense.
Say $E_m$ is the not nowhere dense set, meaning $E_m$ is dense in some ball $B(y_0, r)$ i.e.
$\overline{E_m \cap B(y_0, r)} = B(y_0, r)$. We take advantage of this twice to find solution
approximations in $E_m$.

**Construct approximate solution:**
Let $\varepsilon > 0$ then for any $y\in B(y_0, r)$ there exists $\hat{y} \in E_m$ such that
$||y - \hat{y}|| < \varepsilon$, and there exists $\hat{x}$ such that $L\hat{x} = \hat{y}$
with $||\hat{x}|| \leq m ||\hat{y}||$ and $||y - L\hat{x}|| < \varepsilon$ (in other words $\hat{x}$ is
solution approximation of $Lx = y$), and we have

$$
    ||\hat{x}|| \leq m ||\hat{y}|| \leq m (\varepsilon + r + ||y_0||).
$$

**Map ball of right hand sides to the origin.**
Pick another $y' \in B(y_0, r)$ then we can find another solution approximation $\tilde{x}$
with the same properties above. Then note that $y - y' \in B(0, 2r)$ and that $x = \hat{x} - \tilde{x}$
is a solution approximation with $||Lx - (y - y')|| < 2\varepsilon$ and $||x|| \leq 2n(||y_0| + r + \varepsilon)$.

**Scaling argument.**
Next pick any nonzero $y \in Y$, define $\lambda = \frac{r}{||y||}$ then $\lambda y \in B(0, 2r)$ and there is
an approximate solution $u' \in X$. Define $u = \lambda u'$ and pick $\varepsilon = r / 4$, then $u$ satisfies
$||Lu - y|| < \frac{1}{2} ||y||$ and $||u|| < K ||y||$ where $K:= 2n(5r/4 + ||y_0||) / r$ a constant.

**Iterate.**
Pick $y_0 \in Y$, find $u_1 \in X$ by the previous step, then iterate by defining the residual $y_1 = y_0 - Lu_1$,
and solve for $u_2 \in X$ such that $||Lu_2 - y_1|| < \frac{1}{2}||y_1||$.
We again obtain a convergent series, and we can check similarly to before that its limit
satisfies the required properties.

```


```{prf:remark}

Make sure to take a close look at the proof of the open-mapping theorem. There are three key techniques on display:
(1) **linearity**, (2) **series approximations**, and (3) the **Baire category theorem**.

1. The frequent dilations and translations in the above are allowed by linearity.

2. The series approximation technique has profound signifiance beyond proving results in functional analysis. Take
a look at numerical methods such as gradient descent, conjugate gradient, or even Newton's method. These are all
examples of method that construct solution approximations by constructing approximating series.

3. Finally the completeness of the space $Y$ allows an application of Baire's category theorem, and ensures that
all surjective linear mappings are open, thus we can control the norm of the solution by the norm of the input.

4. There are several important consequence of this theorem. One the {prf:ref}`banach-inverse` is discussed above,
and the closed-graph theorem will be discussed later.

```

