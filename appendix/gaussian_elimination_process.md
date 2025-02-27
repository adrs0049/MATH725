# Gaussian Elimination

Given a $n\times n$ matrix $A$ and vector $b$ we assemble its augmented matrix
and proceed through the following sequence, until the final augmented
matrix is upper triangular.

$$
    \left(\begin{array}{@{}*{1}{c}|c@{}}
        A & b
    \end{array}\right)
    \mapsto
    \left(\begin{array}{@{}*{1}{c}|c@{}}
        A^{(1)} & b^{(1)}
    \end{array}\right) \mapsto
    \left(\begin{array}{@{}*{1}{c}|c@{}}
        A^{(2)} & b^{(2)}
    \end{array}\right) \mapsto
    \dots \mapsto
    \left(\begin{array}{@{}*{1}{c}|c@{}}
        A^{(n-1)} & b^{(n-1)}
    \end{array}\right)
$$

where $A^{(n-1)} = U$ is upper triangular. In more detail, at
each step of this process we eliminate the elements in column
$i$ below the diagonal.

## Step 1: Eliminate the first column

The process begins with the matrix

$$
    \left(\begin{array}{@{}*{1}{c}|c@{}}
        A & b
    \end{array}\right) =
    \left(\begin{array}{cccc|c}
        a_{11} & a_{12} & \dots & a_{1n} & b_1 \\
        a_{21} & a_{22} & \dots & a_{2n} & b_2 \\
        \vdots & \vdots & \ddots & \vdots & \vdots \\
        a_{n1} & a_{n2} & \dots & a_{nn} & b_n \\
    \end{array}\right)
$$

We then eliminate the elements in the first column below the main diagonal by:

**Step 1A**:
Subtracting $\frac{a_{21}}{a_{11}}$ times the first row from the second row. In other words,

$$
    R_2 \mapsto R_2 - \frac{a_{21}}{a_{11}}R_1.
$$

**Step 1B**:
Subtracting $\frac{a_{31}}{a_{11}}$ times the first row from the second row. In other words,

$$
    R_3 \mapsto R_3 - \frac{a_{31}}{a_{11}}R_1.
$$

**And so on until ...**

Subtracting $\frac{a_{n1}}{a_{11}}$ times the first row from the second row. In other words,

$$
    R_n \mapsto R_n - \frac{a_{n1}}{a_{11}}R_1.
$$

This results in the new augmented matrix

$$
    \left(\begin{array}{@{}*{1}{c}|c@{}}
        A^{(1)} & b^{(1)}
    \end{array}\right) =
    \left(\begin{array}{cccc|c}
        a_{11} & a_{12} & \dots & a_{1n} & b_1 \\
        0 & a_{22}^{(1)} & \dots & a_{2n}^{(1)} & b_2^{(1)} \\
        \vdots & \vdots & \ddots & \vdots & \vdots \\
        0 & a_{n2}^{(1)} & \dots & a_{nn}^{(1)} & b_n^{(1)} \\
    \end{array}\right)
$$

## Step 2: Eliminate the second column

Next consider the $(n-1)\times n$ sub-matrix found by ignoring the first row and column of the matrix above. Then repeat the process of eliminating the first column of this sub-matrix.
This gives us

$$
    \left(\begin{array}{@{}*{1}{c}|c@{}}
        A^{(2)} & b^{(2)}
    \end{array}\right) =
    \left(\begin{array}{ccccc|c}
        a_{11}  & a_{12}        & \dots         & \dots     & a_{1n}        & b_1 \\
        0       & a_{22}^{(1)}  & a_{23}^{(1)}  & \dots     & a_{2n}^{(1)}  & b_2^{(1)} \\
        0       & 0             & a_{33}^{(2)}  & \dots     & a_{3n}^{(2)}  & b_3^{(2)} \\
        \vdots  & \vdots        & \vdots        & \ddots    & \vdots        & \vdots \\
        0       & 0             & a_{n3}^{(2)}  & \dots     & a_{nn}^{(2)}  & b_n^{(2)} \\
    \end{array}\right)
$$

**Repeat the previous steps until ...**

## Step n-1: Eliminate the second to last column

We repeat this process $(n-1)$-times until we find

$$
    \left(\begin{array}{@{}*{1}{c}|c@{}}
        A^{(n-1)} & b^{(n-1)}
    \end{array}\right) =
    \left(\begin{array}{ccccc|c}
        a_{11}  & a_{12}        & \dots         & \dots     & a_{1n}            & b_1 \\
        0       & a_{22}^{(1)}  & a_{23}^{(1)}  & \dots     & a_{2n}^{(1)}      & b_2^{(1)} \\
        0       & 0             & a_{33}^{(2)}  & \dots     & a_{3n}^{(2)}      & b_3^{(2)} \\
        \vdots  & \vdots        & \vdots        & \ddots    & \vdots            & \vdots \\
        0       & 0             & 0             & \dots     & a_{nn}^{(n-1)}    & b_n^{(n-1)} \\
    \end{array}\right)
$$

## Algorithm cost

What is the cost of Gaussian Elimination? The matrix
$\left(\begin{array}{@{}*{1}{c}|c@{}} A & b \end{array}\right)$ has size $n \times ( n + 1 )$.
The first step is the  most expensive. We need to eliminate $n-1$
non-zero elements, via $n-1$ row operations. That's a total of

$$
    2(n-1)(n+1),
$$

floating point operations. When we are dealing with row $i$ then there
are $k = n - i + 1$ unknowns left, thus we require

$$
    2(k-1)(k+1) = 2(k^2 - 1)
$$

floating point operations. For the total cost we add up the costs
for each individual step of Gaussian elimination to find

$$
\begin{aligned}
    2\sum_{k=1}^n \left( k^2 - 1\right) &= 2\sum_{k=1}^n k^2 - 2\sum_{k=1}^n 1
        = \frac{1}{3} n(n+1)(2n+1) - 2n \\
        % = \frac{1}{3} n (2n^2 + 3n + 1)
        &= \frac{2}{3}n^3 + n^2 - \frac{5}{3} n.
\end{aligned}
$$


