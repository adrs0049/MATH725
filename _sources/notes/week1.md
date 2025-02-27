# Modern Applied Mathematics

- Development of new mathematical models (modeling).
- **Theoretical analysis of mathematical models.**
- Numerical solutions of these models.
- Data inferences and statistical learning.

Here we will focus on the second point.

---

## Differential equations

We motivate the need for the development of functional analysis through the ubiquitous nature of differential equations. Similar functional analytical techniques are useful when studying stochastic differential equations, and many other applications.

- **ODEs** (ordinary differential equations) are defined by having a finite number of variables of a single independent variable usually $t$.

  For example the following is a linear ODE:

  $$\frac{d \vec{x}}{d t} = A\vec{x}$$

  where $A$ is a $n \times n$ matrix. Then the solution is:

  $$t \mapsto \vec{x}(t) \in \mathbb{R}^n$$

  The space in which the solution of a differential equation "lives" is usually called a **phase-space**.

- **PDEs** require new language.

  - State space is a Banach space of functions.
  - PDEs are operators between Banach spaces.
  - Solutions often arise as weak or weak* limits in these Banach spaces.

- The following reaction-diffusion is an example of a PDE:

  $$\frac{\partial u}{\partial t} = d \Delta u + f(u)$$

  for an unknown function $u(x, t)$. Here $\Delta$ is the Laplacian:

  $$\Delta := \sum_{i = 1}^{n} \frac{\partial^2}{\partial x_i^2}$$

  If we formally introduce the linear operator:

  $$A[u] := d \Delta u$$

  then we can rewrite the PDE as:

  $$\frac{\partial u}{\partial t} = A[u] + f(u)$$

  and it looks like an ODE.

- If the PDE was an ODE we can use the variation of constant formula and the matrix exponential to find a solution i.e.:

  $$u(t) = e^{At} u_0 + \int_0^t e^{A(t-s)} f(u(s)) ds.$$

  **But** here $A$ is a differential operator and not a matrix. Can we define matrix exponentials for unbounded operators? The answer is yes as we will see in the chapter on semigroup theory.

- If $u(x; t)$ is a solution of the "ODE" then we have a mapping:

  $$t \mapsto u(x; t) \in \text{Function Space}.$$

  Thus the phase-space for a PDE is a function space, and the PDE becomes an operator between function spaces. Whether we can invert these operators we will discuss in our chapter on operator theory.

---

Let's discuss the heat / diffusion equation example in a bit more detail. Suppose we have the heat equation on the interval $[0, L]$.

$$\begin{cases}
    u_t &= d u_{xx} \\
    u(t,0) &= u(t, L) = 0 \\
    u(x, 0) &= u_0(x).
\end{cases}$$

Using separation of variables and the principles of superposition we find a solution as a Fourier sine series:

$$u(x, t) = \sum_{k=1}^{\infty} a_n e^{-\lambda_n d t} \sin\left(\frac{n \pi x}{L}\right)$$

The coefficients $a_n$ are determined from the initial condition i.e.:

$$u_0(x) = \sum_{k=1}^{\infty} a_n \sin\left(\frac{n \pi x}{L}\right)$$

and we can use the Fourier trick to solve this equation for $a_n$. Now the family of functions:

$$\mathcal{L}:= \left\{ \sin\left(\frac{n \pi x }{L}\right) : n \in \mathbb{N} \right\}$$

forms an orthogonal set with the inner product:

$$(\phi_n, \phi_m) = \int_0^L \phi_n(x) \phi_m(x) dx$$

Recall that this define a norm via $\|x\| = \sqrt{(x, x)}$. Then $\mathcal{L}$ can be seen as the basis of the function space $L^2(0, L)$ the square integrable functions. Since $\mathcal{L}$ is infinite, $L^2(0, L)$ is an infinite dimensional vector space. Thus we understand the heat equation as an infinite dimensional differential equation.

The final note is that the linear operator $\Delta$ is crucially associated with the boundary conditions. Different boundary conditions lead to different basis and thus different function spaces. Much of PDE theory is concerned with the identification of the correct basis functions and right function spaces. We will come back to this later when discussing operator theory.


