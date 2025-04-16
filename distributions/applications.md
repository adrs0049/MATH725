## Applications to Differential Equations

### Fundamental Solutions

A fundamental solution of a linear differential operator $L$ is a distribution $E$ such that
$LE = \delta$. For example:

- The fundamental solution of the Laplacian $\Delta$ in $\mathbb{R}^3$
is:

$$
    E(x) = -\frac{1}{4\pi |x|}.
$$

- For the heat operator $\partial_t - \Delta$ in $\mathbb{R}^{d+1}$ it is

$$
    E(x, t) =
$$


### Solving PDEs with Distributions

If $E$ is a fundamental solution of $L$ and $f$ is a test function, then
$u = E * f$ solves $Lu = f$.  This provides a powerful method for solving
linear PDEs with constant coefficients.

Put some more examples here.

### Green's Functions

For boundary value problems, Green's functions are analogous to fundamental solutions
but incorporate boundary conditions.

Put some more details here.


## Tempered Distributions and Fourier transform

While beyond the scope of these notes, the theory extends to include:

- Tempered distributions which are those that can be paired with Schwartz functions.
- Fourier transform of distributions.
- Sobolev spaces - function spaces defined using distributions that are crucial in PDE
theory.

**TODO: Expand this.**



