# Duality

:::{tip} Big Idea
To understand a space, study its functionals. The dual space $X^*$ consists of all continuous linear maps $X \to \mathbb{R}$, and the Hahn–Banach theorem guarantees that $X^*$ is rich enough to separate points. Duality gives us weak topologies, reflexivity, and the powerful compactness result of Banach–Alaoglu.
:::

## Overview

There are two ways to study a mathematical structure: look at the objects **in** the space, or look at the functions **on** the space. In functional analysis, the second viewpoint is remarkably powerful.

The dual space $X^* = \mathcal{L}(X, \mathbb{R})$ collects all bounded linear functionals on $X$. Functionals are "measurements"—a scale measures weight, a CT scanner measures line integrals—and $X^*$ captures all possible linear measurements of elements in $X$.

The central result is the **Hahn–Banach Theorem**, which guarantees that functionals defined on subspaces can always be extended to the full space. This leads to:

- **Separation theorems** for convex sets.
- The **Riesz Representation Theorem** identifying dual spaces (e.g., $H^* \cong H$ for Hilbert spaces).
- **Weak and weak-* convergence**, which provide compactness where norm convergence fails.
- **Banach–Alaoglu**, giving weak-* compactness of the unit ball in $X^*$.

## What You Will Learn

- Dual spaces, isomorphisms, and isometries.
- The Hahn–Banach Theorem and its geometric consequences.
- Riesz representation for Hilbert spaces.
- Reflexive spaces and weak convergence.
- Weak-* convergence and the Banach–Alaoglu Theorem.
