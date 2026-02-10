# Distributions and Sobolev Spaces

:::{tip} Big Idea
Classical derivatives don't exist for many functions that arise naturally in PDEs. Distribution theory extends differentiation to all locally integrable functions (and beyond), giving rigorous meaning to objects like the Dirac delta. Sobolev spaces combine this weak differentiability with $L^p$ integrability to create the natural setting for PDE theory.
:::

## Overview

In classical analysis, differentiation requires smoothness. But PDE solutions are often non-smooth—think of shock waves, corners in domains, or fundamental solutions with point singularities. Distribution theory resolves this by shifting the burden of smoothness from the function to the **test functions** it acts on.

A distribution is a continuous linear functional on the space of smooth, compactly supported test functions $\mathcal{D}(\Omega)$. Every locally integrable function defines a distribution, but distributions also include singular objects like the Dirac delta:

$$
\langle \delta, \varphi \rangle = \varphi(0)
$$

This framework lets us:

- Differentiate any distribution, producing another distribution.
- Give meaning to "$-\Delta u = f$" even when $u$ is not twice differentiable.
- Build **Sobolev spaces** $W^{k,p}(\Omega)$ of functions with weak derivatives in $L^p$.

## What You Will Learn

- Test functions, their topology, and the space $\mathcal{D}(\Omega)$.
- Distributions as continuous linear functionals on test functions.
- Operations on distributions: differentiation, multiplication, convolution.
- Mollifiers and approximation by smooth functions.
