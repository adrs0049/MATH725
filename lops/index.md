# Linear Operators

:::{tip} Big Idea
Linear operators are the morphisms of functional analysis—they connect spaces,
encode differential equations, and determine when problems are well-posed. The
three pillars (Banach–Steinhaus, Open Mapping, Closed Graph) give powerful tools
for establishing boundedness and invertibility of operators without explicit
computation.
:::

## Overview

Once we have Banach spaces, the next step is to study **maps between them**. A bounded linear operator $A : X \to Y$ satisfies $\|Ax\|_Y \leq M\|x\|_X$, and the space $\mathcal{L}(X,Y)$ of all such operators is itself a Banach space.

The deep results of this chapter all rely on the **Baire Category Theorem**—a topological result about complete metric spaces. From it we derive:

- **Banach–Steinhaus (Uniform Boundedness):** A pointwise bounded family of operators is uniformly bounded.
- **Open Mapping Theorem:** A surjective bounded operator between Banach spaces is an open map.
- **Closed Graph Theorem:** An operator with a closed graph is automatically bounded.

We also study **compact operators**, which map bounded sets to precompact sets. These operators behave much like matrices in finite dimensions, and their spectral theory is the gateway to Fredholm theory and applications in PDEs.

## What You Will Learn

- Bounded vs. continuous operators and the operator norm.
- The Baire Category Theorem and its consequences.
- Banach–Steinhaus, Open Mapping, and Closed Graph Theorems.
- Compact operators and their spectral properties.
