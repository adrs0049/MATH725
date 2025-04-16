### Connection to Regularization in Physics

This averaging perspective explains why physicists often ``regularize'' singular objects:

- A point charge is represented as $\rho(x) = q\delta(x)$, but physical charges always have
some spatial extent.

- The regularized delta function $\delta_{\epsilon}(x) = \frac{1}{(2\pi\epsilon)^{d/2}}e^{-|x|^2/2\epsilon}$
represents a physical charge distribution.

- As $\epsilon \to 0$ we recover the idealized point charge.

### Scaling Behavior and Physical Dimension

The order of a distribution relates to its scaling behavior, which connects to physical
dimensions. If $T$ is a distribution of order $m$, then under scaling $x \mapsto \lambda x$
we have

$$
\langle T, \phi_\lambda \rangle \sim \lambda^{-d -m} \langle T, \phi \rangle
$$

where $\phi_\lambda(x) = \phi\left( \frac{x}{\lambda} \right).

This scaling relates to the physical dimensions of the quantities represented by distributions.
For instance:

- A density (mass/volume) scales as $\lambda^{-d}$ (order 0).
- A dipole moment scales as $\lambda^{-d-1}$ (order 1).
- Stress tensors and multipole moments have even higher scaling orders.



