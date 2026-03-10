# Duality: Hyperplanes, Functionals, and Hahn–Banach

:::{tip} Big Idea
In a general Banach space there is no inner product, so orthogonality is lost.
What survives is **hyperplane geometry**: every continuous linear functional
slices the space into parallel hyperplanes, and the Hahn–Banach theorem
guarantees there are enough such slices to recover norms, separate points, and
separate convex sets.
:::

## Overview

There are two ways to study a mathematical structure: look at the objects **in**
the space, or look at the functions **on** the space. In functional analysis,
the second viewpoint is remarkably powerful, but it rests on a geometric
foundation that is worth making explicit.

In Hilbert spaces, we have orthogonality: the inner product lets us decompose
vectors into components, project onto subspaces, and find nearest points. But
most Banach spaces have no inner product, so **orthogonality is lost**. What
*does* survive is **hyperplane geometry**. Every continuous linear functional
$f : X \to \mathbb{R}$ slices the space into parallel hyperplanes (the level
sets $f^{-1}(c)$), and its kernel is a codimension-1 subspace. This structure is
purely algebraic and topological; it requires no inner product. The kernel
determines the functional up to scaling, level sets foliate the space, and
closed kernels correspond to continuous functionals. All of this works
identically in $\mathbb{R}^3$ and in $L^p(\Omega)$.

Duality is the systematic study of this surviving geometry. The dual space
$X^* = \mathcal{L}(X, \mathbb{R})$ collects all bounded linear functionals on
$X$, encoding all possible ways to slice the space with hyperplanes. But is
$X^*$ rich enough? Could all functionals miss some structure in $X$? The
**Hahn–Banach Theorem** answers this: functionals defined on subspaces can
always be extended to the full space, guaranteeing that $X^*$ is large enough to
separate points, recover norms, and separate convex sets. From this we get:

- **Separation theorems** for convex sets, putting the hyperplane geometry to
  work.
- The **Riesz Representation Theorem** identifying dual spaces (e.g., $H^* \cong
  H$ for Hilbert spaces), where orthogonality is recovered as a special case.
- **Weak and weak-$*$ convergence**, providing compactness where norm convergence
  fails by testing against functionals.
- **Banach–Alaoglu**, giving weak-$*$ compactness of the unit ball in $X^*$.

## What You Will Learn

- How functionals define hyperplanes, and why kernels have codimension 1.
- The geometry of foliations and what distinguishes continuous from
  discontinuous functionals.
- The Hahn–Banach Theorem and its geometric consequences: separation of convex
  sets and the sup formula for the norm.
- Dual spaces in practice: Riesz representation for Hilbert spaces, reflexive
  and non-reflexive spaces.
- Weak and weak-$*$ convergence, and the Banach–Alaoglu compactness theorem.
