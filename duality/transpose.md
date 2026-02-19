---
exports:
  - format: pdf
    template: plain_latex
    output: exports/transpose.pdf
    id: duality-transpose-pdf
downloads:
  - id: duality-transpose-pdf
    title: Download PDF
---

# The adjoint (transpose) operator


```{prf:definition}
Let $T : X \mapsto Y$ be a continuous linear map, the **transpose / adjoint**
$T^* : Y^* \mapsto X^*$ is defined to be the map that sends any functional
$\lambda \in Y^*$ to

$$ T^* \lambda = \lambda T \quad\implies\quad (T^* \lambda)(x) = \lambda(T(x)) $$

```
