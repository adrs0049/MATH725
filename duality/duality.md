# The Dual-Space

There are two methods to studying mathematical structures.

1. By looking at the objects **in** the space.
2. By looking at functions **on** the space.

Let's see how the second setting looks like in our Banach space setting.

## Introduction

In the Banach space setting the natural mappings to consider are the linear continuous functions between two Banach spaces
$X$ and $Y$. Now consider $\mathcal{L}(X, \mathbb{R})$ the space of bounded linear continuous functionals on $X$.
This is a Banach space, and we will call it the **dual** of $X$ denotes by $X^*$.

The intuitive view is that **functionals** are measurements of an object in the space $X$.

```{prf:example}

We encounter many functionals in daily life.

1. A scale measures the weight of objects i.e. it assigns a real number to each object.
2. A rules measures length.
3. CT-scanners measure line integrals of an unknown tissue density.
4. MRI-scanners measure proton densities along lines.

```

## Isomorphisms and Isometries

First let's explore how we show that two Banach spaces have the same structure. In normed vectorspaces
the **natual map** is $T : X \mapsto Y$. $X, Y$ are equivalent if there exists an invertible continuous
linear map $T : X \mapsto Y$ i.e.

$$ c \|x\|_X \leq \|Tx\|_Y \leq C \|x\|_X $$

Is such a map $T$ exists we say that $X$ and $Y$ are isomorphic. If $c = C = 1$ $T$ is an an **isometry**.


## Intuition Building in $\mathbb{R}^2$.


