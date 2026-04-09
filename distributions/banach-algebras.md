---
kernelspec:
  name: python3
  display_name: Python 3
exports:
  - format: pdf
    template: ./_templates/plain_narrow
    output: exports/banach-algebras.pdf
    id: distributions-banach-algebras-pdf
downloads:
  - id: distributions-banach-algebras-pdf
    title: Download PDF
---

# Sobolev Spaces as Banach Algebras

:::{tip} Big Idea
The spaces $C^0(\overline\Omega)$ and $C^\infty(\overline\Omega)$ are
algebras under pointwise multiplication: the product of two continuous
(or smooth) functions is again continuous (or smooth). Sobolev spaces
inherit this property precisely when they embed into $C^0$, which happens
when $s > d/2$. The algebra structure connects the embedding theory from
the previous chapter to the bandedness of multiplication operators in
spectral methods.
:::

## Why multiplication matters

So far we have used Sobolev spaces as *linear* function spaces: we add
functions, take limits, and apply linear operators. But functions can also be
**multiplied**, and a natural question arises: when is the pointwise product
$uv$ again in the same Sobolev space? The answer turns out to connect the
embedding theory we just developed to the structure of multiplication operators
in spectral methods.


## The algebra property from embeddings

An **algebra** over $\mathbb{R}$ (or $\mathbb{C}$) is a vector space $A$ that
also carries a **multiplication**, a bilinear map $A \times A \to A$ that is
compatible with the linear structure. You already know several:

| Space | Multiplication | Submultiplicative norm? |
|---|---|---|
| $\mathbb{R}^{n \times n}$ | Matrix product | $\|AB\| \leq \|A\|\|B\|$ (operator norm) |
| $C[0,1]$ | Pointwise: $(fg)(x) = f(x)g(x)$ | $\|fg\|_\infty \leq \|f\|_\infty \|g\|_\infty$ |
| $L^\infty(\Omega)$ | Pointwise a.e. | $\|fg\|_\infty \leq \|f\|_\infty \|g\|_\infty$ |
| $\ell^1(\mathbb{Z})$ | Convolution | $\|f * g\|_1 \leq \|f\|_1 \|g\|_1$ (Young) |

A **Banach algebra** is a Banach space whose norm is **submultiplicative**:
$\|uv\| \leq C\|u\|\|v\|$. This single inequality says that the multiplication
is *continuous* as a bilinear map, or equivalently, that the space is **closed
under multiplication** with quantitative control.

Not every function space is an algebra. The product of two $L^2$ functions is
generally only in $L^1$ (by Cauchy--Schwarz, $\|fg\|_{L^1} \leq
\|f\|_{L^2}\|g\|_{L^2}$, but $fg$ need not be in $L^2$). So $L^2$ with
pointwise multiplication is *not* an algebra; multiplication takes you
outside the space. The question for Sobolev spaces is: **does the extra
regularity fix this?**

The key observation is that $C^0(\overline\Omega)$ *is* a Banach algebra
(the sup norm is submultiplicative), so any Banach space that embeds
continuously into $C^0$ inherits the algebra property. If
$X \hookrightarrow C^0$ with $\|u\|_\infty \leq C\|u\|_X$, then

$$\|uv\|_X \leq C'\|u\|_X \|v\|_X$$

whenever the product rule and embedding estimate can be combined. The
Sobolev embedding theorem ({prf:ref}`sobolev-embedding-theorem`) gives
$H^s \hookrightarrow C^0$ exactly when $s > d/2$. This is the threshold.

```{prf:theorem} Sobolev multiplication (Banach algebra property)
:label: sobolev-banach-algebra

Let $\Omega \subseteq \mathbb{R}^d$ be open with Lipschitz boundary (or
$\Omega = \mathbb{R}^d$). If $s > d/2$, then $H^s(\Omega)$ is a **Banach
algebra** under pointwise multiplication: there exists a constant $C > 0$
such that

$$\|uv\|_{H^s} \leq C \, \|u\|_{H^s} \, \|v\|_{H^s} \quad \text{for all } u, v \in H^s(\Omega).$$

In particular, $H^s(\Omega)$ is closed under multiplication.
```

````{prf:proof}
:class: dropdown

We prove the case $s = k$ a positive integer; the fractional case requires
interpolation. The strategy is to apply the **Leibniz rule** (product rule for
higher derivatives) and then split each term so that one factor is controlled
in $L^\infty$ via the Sobolev embedding.

**Step 1: Leibniz rule.** For any multi-index $|\alpha| \leq k$, the general
Leibniz rule gives

$$D^\alpha(uv) = \sum_{\beta \leq \alpha} \binom{\alpha}{\beta} D^\beta u \cdot D^{\alpha - \beta} v.$$

This is the higher-dimensional product rule: it distributes the $\alpha$
derivatives between $u$ and $v$ in all possible ways. (For $k = 1$ in one
dimension, this is simply $(uv)' = u'v + uv'$.)

**Step 2: Estimating each term.** Each term in the Leibniz sum has the form
$D^\beta u \cdot D^{\alpha - \beta} v$ where $|\beta| + |\alpha - \beta| =
|\alpha| \leq k$. We estimate in $L^2$ using Hölder's inequality with
exponents $2$ and $\infty$:

$$\|D^\beta u \cdot D^{\alpha - \beta} v\|_{L^2} \leq \|D^\beta u\|_{L^2} \, \|D^{\alpha-\beta} v\|_{L^\infty}.$$

Since $|\alpha - \beta| \leq k$ and $k > d/2$, the function $D^{\alpha -
\beta} v$ has at least $k - |\alpha - \beta|$ remaining derivatives in $L^2$.
When $|\alpha - \beta| \leq k$, we can apply the Sobolev embedding to get

$$\|D^{\alpha-\beta} v\|_{L^\infty} \leq C \, \|v\|_{H^k}.$$

(More precisely, $D^{\alpha - \beta} v \in H^{k - |\alpha - \beta|}$ and for the
terms where $k - |\alpha - \beta| > d/2$ we embed directly into $L^\infty$;
for the remaining terms we swap the roles of $u$ and $v$.)

**Step 3: Combining.** Summing over all $|\alpha| \leq k$ gives

$$\|uv\|_{H^k} = \sum_{|\alpha| \leq k} \|D^\alpha(uv)\|_{L^2} \leq C \sum_{|\alpha| \leq k} \sum_{\beta \leq \alpha} \|D^\beta u\|_{L^2} \, \|v\|_{H^k} \leq C' \, \|u\|_{H^k} \, \|v\|_{H^k}.$$

````

```{prf:example} $H^1$ in one dimension
:label: ex-h1-banach-algebra

For $d = 1$ and $s = 1$, the condition $s > d/2$ becomes $1 > 1/2$, which
holds. The proof is completely explicit:

$$\|uv\|_{H^1} = \|uv\|_{L^2} + \|(uv)'\|_{L^2}.$$

For the first term: $\|uv\|_{L^2} \leq \|u\|_{L^\infty} \|v\|_{L^2}$. For
the second, the product rule gives $(uv)' = u'v + uv'$, so

$$\|(uv)'\|_{L^2} \leq \|u'\|_{L^2} \|v\|_{L^\infty} + \|u\|_{L^\infty} \|v'\|_{L^2}.$$

By the Sobolev embedding $H^1(0,1) \hookrightarrow C[0,1]$, we have
$\|u\|_{L^\infty} \leq C\|u\|_{H^1}$ and similarly for $v$. Combining:

$$\|uv\|_{H^1} \leq C \|u\|_{H^1} \|v\|_{H^1}.$$

Each term in the estimate pairs **derivatives on one factor** with
**$L^\infty$ control on the other**. The Sobolev embedding converts the
$L^\infty$ norms into $H^1$ norms, closing the estimate.
```

```{prf:remark} Why $s > d/2$ is sharp
:label: rem-banach-algebra-sharp
:class: dropdown

The threshold $s > d/2$ cannot be improved. For $s = d/2$, the space
$H^{d/2}(\mathbb{R}^d)$ does **not** embed into $L^\infty$ (functions in
$H^{d/2}$ can have logarithmic singularities), and multiplication fails to
be continuous. For instance, in $d = 2$, the function $u(x) =
\log\log(1/|x|)$ near the origin belongs to $H^1(\Omega)$ but $u^2$ does
not.
```


## Multiplication in frequency space: why regularity implies bandedness

The Banach algebra property tells us that multiplication by $u \in H^s$ is a
bounded operator on $H^s$. But *what does this operator look like* when we
expand in a spectral basis? The answer reveals a striking structural property:
**regularity forces approximate bandedness**.

To see this most cleanly, work on the torus $\mathbb{T} = [0, 2\pi)$ with
Fourier basis $\{e_k(x) = e^{ikx}\}_{k \in \mathbb{Z}}$. Expand
$u = \sum_k \hat{u}_k e_k$. The multiplication operator $M_u : v \mapsto uv$
has the matrix representation

$$(M_u)_{jk} = \langle M_u e_k, e_j \rangle = \langle u \cdot e_k, e_j \rangle = \hat{u}_{j-k}.$$

```{prf:observation} Multiplication is convolution in frequency
:label: obs-mult-convolution

The matrix of $M_u$ in the Fourier basis is a **Toeplitz matrix**: the
$(j,k)$-entry depends only on $j - k$, and equals the Fourier coefficient
$\hat{u}_{j-k}$. Multiplying by $u$ in physical space is convolution by
$\hat{u}$ in frequency space.
```

Now the connection to regularity becomes immediate. If $u \in H^s$, then

$$\sum_{k} (1 + k^2)^s |\hat{u}_k|^2 < \infty \quad \Longrightarrow \quad |\hat{u}_k| \lesssim |k|^{-s-1/2} \text{ (by Cauchy--Schwarz)}.$$

In particular, the off-diagonal entries of $M_u$ decay:

$$|(M_u)_{jk}| = |\hat{u}_{j-k}| \lesssim |j - k|^{-s - 1/2}.$$

```{prf:proposition} Off-diagonal decay of multiplication matrices
:label: prop-offdiag-decay

Let $u \in H^s(\mathbb{T})$ with $s \geq 0$. The multiplication operator $M_u$
in the Fourier basis satisfies

$$|(M_u)_{jk}| \leq \frac{C \|u\|_{H^s}}{(1 + |j-k|)^{s+1/2}}.$$

In particular:
- $u \in H^1$: entries decay like $|j-k|^{-3/2}$, so off-diagonal entries are
  summable.
- $u \in H^2$: decay like $|j-k|^{-5/2}$, giving rapid off-diagonal decay.
- $u \in C^\infty$: superalgebraic decay, meaning the matrix is **numerically banded**
  (entries drop below machine precision within a few diagonals).
- $u$ analytic: **exponential** off-diagonal decay, making it essentially a banded
  matrix.
```

The following picture makes this concrete.

```{code-cell} ipython3
:tags: [hide-input]

import numpy as np
import matplotlib.pyplot as plt
from matplotlib.colors import LogNorm

fig, axes = plt.subplots(1, 3, figsize=(15, 4.5))

N = 64  # number of Fourier modes

# --- Three functions with increasing regularity ---
k = np.arange(-N//2, N//2)

# 1. Step function (discontinuous, in H^{1/2-ε})
u_hat_step = np.zeros(N, dtype=complex)
for j in range(N):
    kj = k[j]
    if kj != 0:
        u_hat_step[j] = (1 - (-1.0)**kj) / (1j * np.pi * kj)

# 2. Hat function (Lipschitz, in H^1)
u_hat_hat = np.zeros(N, dtype=complex)
for j in range(N):
    kj = k[j]
    if kj != 0:
        u_hat_hat[j] = 2 * (1 - np.cos(np.pi * kj / 2)) / (np.pi * kj)**2
    else:
        u_hat_hat[j] = 0.5

# 3. Gaussian (analytic)
sigma = 0.3
u_hat_gauss = np.exp(-sigma**2 * k**2 / 2)
u_hat_gauss = u_hat_gauss / np.max(np.abs(u_hat_gauss))

functions = [
    (u_hat_step, 'Step function\n(discontinuous)'),
    (u_hat_hat, 'Hat function\n($H^1$, Lipschitz)'),
    (u_hat_gauss, 'Gaussian\n(analytic)')
]

for ax, (u_hat, title) in zip(axes, functions):
    # Build Toeplitz multiplication matrix
    M = np.zeros((N, N), dtype=complex)
    # Shift to standard ordering for building Toeplitz matrix
    u_hat_shifted = np.fft.fftshift(u_hat)
    for j in range(N):
        for l in range(N):
            idx = (j - l) % N
            M[j, l] = u_hat_shifted[idx]

    absM = np.abs(M)
    absM = np.maximum(absM, 1e-16)  # floor for log scale

    im = ax.imshow(absM[:32, :32], norm=LogNorm(vmin=1e-10, vmax=absM.max()),
                   cmap='viridis', aspect='equal')
    ax.set_title(title, fontsize=11)
    ax.set_xlabel('Column $k$', fontsize=10)
    ax.set_ylabel('Row $j$', fontsize=10)
    ax.tick_params(labelsize=8)
    plt.colorbar(im, ax=ax, fraction=0.046, pad=0.04)

plt.suptitle(r'Multiplication matrices $|(M_u)_{jk}| = |\hat{u}_{j-k}|$: regularity $\to$ bandedness',
             fontsize=12, y=1.02)
plt.tight_layout()
plt.show()
```

*The multiplication matrix in the Fourier basis for three functions of
increasing regularity. Left: a step function (discontinuous) produces a
full, slowly-decaying matrix. Center: a hat function ($H^1$) produces
algebraic off-diagonal decay. Right: a Gaussian (analytic) produces
exponential decay, so the matrix is effectively banded. The color scale is
logarithmic.*


### The intuition: regularity is frequency localization

Why should smoothness produce banded multiplication matrices? The intuition
comes from **three equivalent ways to say the same thing**:

1. **Regularity = frequency concentration.** A function in $H^s$ has Fourier
   coefficients decaying like $|k|^{-s-1/2}$. Higher regularity means the
   function's energy is *concentrated at low frequencies*.

2. **Multiplication = convolution in frequency.** The matrix $M_u$ is Toeplitz
   with entries $\hat{u}_{j-k}$. Applying $M_u$ to a vector of Fourier
   coefficients is **convolution** with the sequence $(\hat{u}_k)$.

3. **Convolving with something narrow produces something narrow.** If the
   sequence $(\hat{u}_k)$ is concentrated near $k = 0$ (because $u$ is
   smooth), then convolution with it only couples mode $k$ to nearby modes
   $k \pm \Delta k$, which is exactly the statement that $M_u$ is approximately banded.

Putting these together: **smooth functions act locally in frequency space**.
Multiplying by a smooth function is like a *short-range interaction* between
Fourier modes. Multiplying by a rough function is a long-range interaction
that couples all modes to all other modes.

```{prf:remark} Analogy with integral operators
:label: rem-integral-operator-analogy
:class: dropdown

This pattern is familiar from integral operators. A kernel $K(x,y)$ produces
a banded matrix in some basis when the kernel is "close to diagonal." For
multiplication, the kernel is $K(x,y) = u(x) \delta(x - y)$, which is as diagonal as
possible in physical space. But expanding in the Fourier basis, this perfectly
diagonal operator becomes the Toeplitz matrix $\hat{u}_{j-k}$, which is
banded only when $u$ is smooth. The same operator can be diagonal in one
basis and banded in another; the bandedness in frequency reflects the
smoothness in space.
```


### Connection to spectral and collocation methods

This structure is exactly what makes **spectral methods** efficient for smooth
problems.

In a pseudospectral (collocation) method, we want to compute the Fourier (or
Chebyshev) coefficients of a product $uv$. The naive approach is to form
$M_u$ and multiply, an $O(N^2)$ operation. But the collocation approach
exploits a factorization:

$$M_u = F^{-1} \, \operatorname{diag}(\mathbf{u}) \, F$$

where $F$ is the DFT matrix and $\operatorname{diag}(\mathbf{u})$ contains the
values of $u$ at collocation points. **Multiplication is diagonal in physical
space**, so we:

1. Transform $\hat{v} \to v$ at collocation points (inverse FFT, $O(N \log N)$),
2. Multiply pointwise: $w_j = u_j v_j$ ($O(N)$),
3. Transform back $w \to \hat{w}$ (forward FFT, $O(N \log N)$).

The total cost is $O(N \log N)$ instead of $O(N^2)$. But here is the subtle
point: this procedure is exact only for trigonometric polynomials of degree
$\leq N$. For general smooth functions, the product $uv$ may have Fourier
modes up to degree $2N$, and the modes above $N$ get **aliased** back into
the $[-N, N]$ range.

The Banach algebra property tells us this aliasing is harmless for smooth
functions: since $|\hat{u}_k| \lesssim |k|^{-s-1/2}$, the aliased modes are
exponentially small (for analytic $u$) or at least rapidly decaying (for
Sobolev $u$). The error from aliasing is controlled by the off-diagonal decay
of $M_u$, precisely the entries we truncate by working with a finite matrix.

```{prf:remark} Chebyshev vs. Fourier
:label: rem-chebyshev-multiplication
:class: dropdown

For Chebyshev spectral methods, the multiplication matrix is not Toeplitz but
**almost-banded**: the Chebyshev expansion $u = \sum_k a_k T_k$ gives a
multiplication matrix with entries involving the *linearization coefficients*
of Chebyshev products ($T_j T_k = \frac{1}{2}(T_{j+k} + T_{|j-k|})$), and
the matrix has the same off-diagonal decay governed by the rate of decay of the
Chebyshev coefficients $a_k$. The story is identical: regularity of $u$
controls the coefficient decay, which controls the bandwidth. This is the
algebraic reason why collocation methods produce banded or nearly-banded
discrete operators for smooth problems.
```

```{prf:remark} The Banach algebra property as a spectral guarantee
:label: rem-banach-algebra-spectral
:class: dropdown

From the numerical analyst's perspective, the Banach algebra property of $H^s$
is a **stability guarantee for nonlinear spectral methods**: if $u, v \in H^s$
and you form their product spectrally (with or without aliasing), the result
stays in $H^s$ with a controlled norm. This is essential for the convergence
theory of spectral methods applied to nonlinear PDEs: it ensures that the
nonlinearity does not create uncontrolled high-frequency content that would
destabilize the computation.
```
