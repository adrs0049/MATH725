---
exports:
  - format: pdf
    template: plain_latex
    output: exports/open-map.pdf
    id: lops-open-map-pdf
downloads:
  - id: lops-open-map-pdf
    title: Download PDF
---

# The Open Mapping Theorem

The open-mapping theorem is another of the big theorems of functional analysis. Its significance is that
it equates qualitative solvability of a linear problem $Lx = y$ with quantitative solvability.
We will begin by stating the qualitative version and explore its consequences on the solvability of
linear operators, followed by the quantitative version.

```{prf:definition} Open map
:label: def-open-map

A map $f : X \to Y$ between topological spaces is called **open** if it maps open sets to open sets, i.e. $f(U)$ is open in $Y$ whenever $U$ is open in $X$.
```

Geometrically, openness means **the image of every ball contains a ball**: sets with interior keep their interior, nothing gets crushed to zero volume. A map that is not open flattens the unit ball into something with empty interior, and any attempt to invert such a map is necessarily discontinuous since small perturbations in $Y$ can jump to distant points in $X$.

```{prf:theorem} Open Mapping Theorem
Let $U, V$ be the open unit balls of the Banach spaces $X, Y$ respectively. To every bounded linear
operator $L$ of $X$ **onto** $Y$ there corresponds $\delta > 0$ so that
$L(U) \supset \delta V = \{ y \in Y : ||y|| < \delta \}.$
```

The quantitative content is that there is a *uniform* lower bound $B_\delta(0) \subset L(B_1(0))$ on how much volume survives. In the bijective case, $\delta = 1/\|L^{-1}\|_{\mathrm{op}}$. By the linearity of $L$ this extends to all open sets: $L$ maps every open set to an open set, i.e. $L$ is an open mapping.

````{prf:corollary} Banach's Bounded Inverse Theorem
:label: banach-inverse

Let $L$ be a linear operator between two Banach spaces $X$ and $Y$, that is **onto** and one-to-one, then
$L^{-1}$ is a bounded linear operator.

```{dropdown} **Proof:**
By the Open Mapping Theorem, $L$ is an open map. Recall that a map $f : Y \to X$ is continuous if and only if the preimage of every open set is open. The preimage of an open set $U \subseteq X$ under $L^{-1}$ is

$$(L^{-1})^{-1}(U) = L(U),$$

since $L^{-1}(y) \in U \iff y \in L(U)$. The Open Mapping Theorem says $L(U)$ is open for every open $U$, so $(L^{-1})^{-1}(U)$ is open for every open $U$, which is precisely the definition of $L^{-1}$ being continuous. A continuous linear map is bounded, so $L^{-1}$ is bounded.
```
````

The previous statement is remarkable in the sense that it lifts our intuition about linear operators
in finite dimensions (i.e. that bijectiveness is equivalent to invertibility) to the infinite dimensional
case.

````{prf:corollary} Equivalence of norms
:label: cor-equiv-norms

If $\|\cdot\|_1$ and $\|\cdot\|_2$ are two norms on a vector space $X$, both making it a Banach space, and $\|x\|_2 \leq C\|x\|_1$ for all $x$, then the norms are equivalent: there exists $C' > 0$ such that $\|x\|_1 \leq C'\|x\|_2$ for all $x$.

```{dropdown} **Proof:**
The identity map $\mathrm{id} : (X, \|\cdot\|_1) \to (X, \|\cdot\|_2)$ is bounded (by assumption), linear, and bijective. Both spaces are Banach. By {prf:ref}`banach-inverse`, $\mathrm{id}^{-1} : (X, \|\cdot\|_2) \to (X, \|\cdot\|_1)$ is bounded, giving the reverse inequality.
```
````

```{prf:remark}
:class: dropdown

Normally, proving norm equivalence requires two inequalities. This corollary says that if both norms make the space complete, one inequality gives you the other for free. In particular, you cannot have two genuinely different Banach space topologies on the same space where one is strictly finer than the other: if a stronger norm and a weaker norm both give completeness, they must be equivalent.
```

## Why Does the Open Mapping Theorem Need Completeness?

In finite dimensions the Open Mapping Theorem is almost trivial: compactness of the unit ball does all
the work. In infinite dimensions compactness fails, and completeness must substitute via Baire's
category theorem. The details below make this precise.

::::{dropdown} **The Finite-Dimensional Story**

Every continuous linear surjection $T : \mathbb{R}^n \to \mathbb{R}^m$ is automatically an open map.
The argument is almost purely geometric:

1. **Surjectivity gives absorbing.** The image $T(B)$ of the open unit ball is convex, balanced
   (symmetric about $0$), and *absorbing*: for every $y \in \mathbb{R}^m$, some scalar multiple
   $\lambda y$ lies in $T(B)$. This follows immediately from surjectivity: given $y$, pick $x$ with
   $Tx = y$, then $y/\|x\| = T(x/\|x\|) \in T(B)$.

2. **Absorbing + convex + balanced $\implies$ nonempty interior (in finite dimensions).** Pick a basis
   $e_1, \dots, e_m$ of $\mathbb{R}^m$. Since $T(B)$ is absorbing, for each $i$ there exists
   $\lambda_i > 0$ with $\lambda_i e_i \in T(B)$. By convexity and symmetry, $T(B)$ contains the
   convex hull of $\{\pm \lambda_1 e_1, \dots, \pm \lambda_m e_m\}$. This is a cross-polytope (a
   "diamond"), a solid body in $\mathbb{R}^m$ with nonempty interior.

3. **Nonempty interior at the origin $\implies$ openness.** Once $T(B)$ contains an open ball around
   $0$, linearity propagates this to all open sets: $T$ maps every open set to an open set.

The deeper reason this works is **compactness of the unit ball** (Heine–Borel). Compact $\to$
continuous images are compact $\to$ compact convex sets with the right spanning properties have
interior. Everything closes cleanly because there are only finitely many directions to account for.

::::

::::{dropdown} **What Breaks in Infinite Dimensions**

By Riesz's lemma, the closed unit ball in an infinite-dimensional Banach space is never compact, destroying the finite-dimensional argument at its root. In finite dimensions, compressing finitely many coordinate directions by positive factors always leaves a solid body with nonempty interior; in infinite dimensions, compressions $\lambda_n \to 0$ can crush the image to a set with empty interior, even though every finite-dimensional projection still looks fine.

### A concrete example

Let $c_{00}$ be the space of real sequences with only finitely many nonzero
terms, equipped with the sup-norm $\|x\|_\infty = \sup_k |x_k|$. As we saw in
the Banach-Steinhaus discussion, $c_{00}$ is **not complete**.

Define $T : c_{00} \to c_{00}$ by

$$
T\left(\{x_n\}\right) = \left\{\frac{x_n}{n}\right\}.
$$

This is bounded ($\|Tx\|_\infty \leq \|x\|_\infty$). It compresses each coordinate direction by a different factor: the $n$-th direction is scaled by $\lambda_n = 1/n$, so the compressions tend to zero as $n \to \infty$.

**Bijective on $c_{00}$:** Injectivity is immediate: if $Tx = 0$ then $x_n/n = 0$ for all $n$, so $x = 0$. For surjectivity, given $y \in c_{00}$, set $x_n = ny_n$. Since $y$ has finite support, so does $x$, hence $x \in c_{00}$ and $Tx = y$.

**Not open:** For any $\varepsilon > 0$, the vector $\frac{\varepsilon}{2} e_k$ lies in $B_\varepsilon(0)$. Its unique preimage under $T$ is $\frac{k\varepsilon}{2} e_k$, which has norm $k\varepsilon/2 \to \infty$ as $k \to \infty$. So no matter how small $\varepsilon$ is, $B_\varepsilon(0)$ contains points whose preimages escape any fixed ball. Equivalently, $T(B)$ is the set $\{y \in c_{00} : |y_k| < 1/k\}$, an "infinite-dimensional box" that gets narrower in each successive direction. No sup-norm ball fits inside it.

**What happens on the completion?** On $c_0$, the map $T$ is no longer surjective: $y = \{1/n\} \in c_0$ requires $x_n = 1$ for all $n$, but the constant sequence $\{1, 1, 1, \ldots\} \notin c_0$. So surjectivity fails on the completion, and the OMT hypothesis is no longer met.

::::

## Quantitative Formulation

Surjectivity alone is qualitative: "solutions exist." Openness adds quantitative content: "solutions exist *with controlled norm*," i.e. there is a constant $C$ such that every $y$ has a preimage $x$ with $\|x\| \leq C\|y\|$. The Bounded Inverse Theorem sharpens this further when $L$ is also injective: the preimage is unique and $\|x\| \leq \|L^{-1}\|_{\mathrm{op}} \|y\|$.

In finite dimensions, a bijective linear map is automatically invertible with a bounded inverse. In infinite dimensions this fails: the $c_{00}$ counterexample above is a bounded bijection whose inverse is unbounded. "Invertible" should really mean *stably* invertible, i.e. $L^{-1}$ is also bounded. The Open Mapping Theorem is the bridge: for Banach spaces, surjectivity + boundedness automatically yields openness, and openness + injectivity gives a bounded inverse. So the algebraic notion of invertibility (bijection) coincides with the analytic notion (bounded inverse), but only in the Banach space setting.

This is why the Open Mapping Theorem matters so much for PDEs: it is not enough to know $Lu = f$ has a solution. You need to know $\|u\| \leq C\|f\|$, that the solution depends continuously on the data. Open Mapping says surjectivity *automatically* gives you this stability, as long as you are working in Banach spaces.

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
:class: dropdown

Make sure to take a close look at the proof of the open-mapping theorem. There are three key techniques on display:
(1) **linearity**, (2) **series approximations**, and (3) the **Baire category theorem**.

1. The frequent dilations and translations in the above are allowed by linearity.

2. The series approximation technique has profound significance beyond proving results in functional analysis. Take
a look at numerical methods such as gradient descent, conjugate gradient, or even Newton's method. These are all
examples of methods that construct solution approximations by constructing approximating series.

3. Completeness enters twice. **Completeness of $Y$** feeds Baire's theorem: surjectivity gives $Y = \bigcup_n \overline{T(nB_X)}$, and Baire forces at least one of these closed sets to have nonempty interior, so $\overline{T(B_X)}$ contains a ball. **Completeness of $X$** then promotes from the closure to the set itself: approximate preimages are assembled into a geometrically decreasing series whose partial sums are Cauchy, and completeness guarantees convergence to an exact preimage with controlled norm. In the $c_{00}$ counterexample, each $\overline{T(nB)} = \{y : |y_k| \leq n/k\}$ is nowhere dense (perturb the $k$-th coordinate for large $k$ to escape), so $c_{00}$ is covered by nowhere dense sets. Baire forbids this in a complete space, but $c_{00}$ is incomplete, so the argument has no traction.

```

```{prf:remark} Condition numbers
:class: dropdown

In numerical linear algebra, the central quantity controlling stability of solving $Lx = y$ is the **condition number** $\kappa(L) = \|L\| \cdot \|L^{-1}\|$. If the right-hand side $y$ is perturbed by relative error $\varepsilon$, the solution can be perturbed by up to $\kappa(L) \cdot \varepsilon$. For finite-dimensional invertible matrices, $\kappa(A) < \infty$ automatically, and the whole game is about *how large* $\kappa$ is. In infinite dimensions, the Bounded Inverse Theorem is what guarantees $\|L^{-1}\|_{\mathrm{op}} < \infty$ (and hence $\kappa(L) < \infty$) *at all*. The Open Mapping Theorem is the qualitative floor beneath condition numbers: it says the problem is well-conditioned before you even start worrying about how well-conditioned it is.

This has far-reaching consequences for numerical methods. When we discretize $Lu = f$ by a sequence of finite-rank operators $L_n$ and solve $L_n u_n = f_n$, the Open Mapping Theorem guarantees well-posedness of the continuous problem, Banach-Steinhaus guarantees stability of convergent schemes (this is the content of the **Lax equivalence theorem**: convergence $\iff$ stability), and the Neumann series controls condition numbers of the discrete problems. We will return to these connections in the applications.
```

