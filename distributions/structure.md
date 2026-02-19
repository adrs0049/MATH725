---
exports:
  - format: pdf
    template: plain_latex
    output: exports/structure.pdf
    id: distributions-structure-pdf
downloads:
  - id: distributions-structure-pdf
    title: Download PDF
---

## Support and Locality

### Support of a Distribution

A distribution $T$ is said to be supported in a closed set $K$ if $\langle T, \phi \rangle = 0$
for all $\phi \in \mathcal{C}_c^{\infty}(\mathbb{R}^d)$ with
$\text{supp}(\phi) \cap K = \emptyset$.

The support of $T$, denoted $\text{supp}(T)$, is the smallest set $K$ such that $T$ is supported
in $K$.

```{prf:exmaple}

- The support of the Dirac delta is $\text{supp}(\delta) = \{ 0 \} $.
- If $f$ is a continuous function, $\text{supp}(T_f) = \overline{\{ x : f(x) \neq 0 \}}$.

```

### Local Structure

Two distributions $T_1$ and $T_2$ are equal on an open set $\Omega$ if
$\langle T_1, \phi \rangle = \langle T_2, \phi \rangle$ for all $\phi$.

If $T_f$ is a regular distribution and $T_f = 0$ on an open set $\Omega$, then $f = 0$
almost everywhere on $\Omega$.

### Distributions with Point Support

A fundamental result: If $T$ is a distribution supported at a single point $x_0$, then
$T$ is a finite linear combination of derivatives of the delta function at $x_0$:

$$
    T = \sum_{|\alpha| \leq m} c_{\alpha} D^\alpha \delta_{x_0}
$$

where $m$ is the order of $T$.


## The Structure Theorem for Distributions


