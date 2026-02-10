# Function Spaces and Foundations

:::{tip} Big Idea
PDEs look like ODEs—if you squint. The key insight of functional analysis is to
treat solutions as points in infinite-dimensional function spaces, where
differential operators become linear maps between Banach spaces. This
abstraction lets us port finite-dimensional intuition (eigenvalues, convergence,
compactness) to the PDE world.
:::

## Overview

Why do we need functional analysis? Consider a reaction-diffusion equation:

$$
\frac{\partial u}{\partial t} = d \Delta u + f(u)
$$

If we set $A[u] := d\Delta u$, this looks like the ODE $\dot{x} = Ax + f(x)$. For ODEs, solutions live in $\mathbb{R}^n$—a finite-dimensional space with a well-understood theory. But PDE solutions live in **infinite-dimensional function spaces**, and much of finite-dimensional intuition breaks down:

- Not all norms are equivalent.
- Bounded closed sets need not be compact.
- Convergence comes in many flavors (strong, weak, weak-*).

This chapter sets up the language and tools needed to work in these spaces: norms, completeness, density, separability, and compactness.

## What You Will Learn

- How to define and compare norms on function spaces ($L^p$, $C^k$, Sobolev).
- Completeness and Banach spaces—why we need them and how to verify them.
- Density and approximation—mollifiers, Weierstrass approximation.
- Compactness in infinite dimensions—Arzelà–Ascoli and why bounded sequences don't always have convergent subsequences.
