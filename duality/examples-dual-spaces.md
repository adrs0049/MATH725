---
exports:
  - format: pdf
    template: plain_latex
    output: exports/examples-dual-spaces.pdf
    id: duality-examples-dual-spaces-pdf
downloads:
  - id: duality-examples-dual-spaces-pdf
    title: Download PDF
---

# Examples of dual-spaces

There are three **main** classes of duality.

1. **Hilbert spaces** are **self-dual** i.e. $X = X^*$.
   The geometric view is that each functional corresponds directly to an element in $X$.

   ```{prf:example}

   In $\mathbb{R}^n$ each functional arises via the inner product, thus $(\mathbb{R}^n)^* = \mathbb{R}^n$.
   Similarly, for $\mathbb{C}^n$.

   ```

   ```{prf:example}

   In $L^2(\Omega)$ every functional is given by

   $$ f[x] = \int x(t) g(t) \mathrm{d}t,\quad\mbox{for some}\ g \in L^2(\Omega). $$

   ```

2. **Reflexive spaces** are those for which $X^{**} = X$.

   ```{prf:example}

   The spaces $L^p(\Omega)$ for $1 < p < \infty$ are reflexive with
   $(L^p)^* = L^q$ where $\frac{1}{p} + \frac{1}{q} = 1$.

   ```

3. **Non-reflexive spaces** are those where $X \subset X^{**}$.

   ```{prf:example}

   $L^\infty(\Omega)$ is not separable i.e. it has too many independent directions.
   From the previous result we would guess that $(L^\infty)^* = L^1$ however we know
   that functions in $L^1$ correspond to regular measures on $\Omega$. But this won't
   let us distinguish / measure functions in $L^\infty$, recall that the topology i.e.
   norm on $L^\infty$ is very discrening. Thus we need singular measure function properties
   on sets of measure zero.

   ```
