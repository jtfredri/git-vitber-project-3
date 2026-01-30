### Numerical Solution of the Cahn–Hilliard Equation

This notebook contains numerical solvers for the two–dimensional Cahn–Hilliard equation using Fourier spectral methods in space and implicit–explicit (IMEX) time discretizations. The implementation includes verification via the method of manufactured solutions, convergence studies, and physical diagnostics such as mass conservation and energy decay.

### The Cahn–Hilliard Equation

We consider the Cahn–Hilliard equation on a periodic domain $\Omega = [0,L_x)\times[0,L_y)$:

$$
\partial_t u + \kappa \Delta^2 u - a \Delta u = \Delta\!\left(u^3 - (1+a)u\right) + g(x,y,t),
$$

where $u(x,y,t)$ is the concentration field, $\kappa > 0$ is the interface parameter, $a \ge 0$ is a splitting parameter, and $g(x,y,t)$ is a prescribed source term.

### Backward Euler IMEX Scheme

Let $\tau$ denote the time step size and $t_n = t_0 + n\tau$.  
The backward Euler IMEX discretization computes $u^{n+1}$ from $u^n$ using the equation

$$
\frac{u^{n+1} - u^n}{\tau} + \kappa \Delta^2 u^{n+1} - a \Delta u^{n+1} - g^{n+1} = \Delta\!\left((u^n)^3 - (1+a)u^n\right).
$$

Here the linear terms are treated implicitly, while the nonlinear term is treated explicitly.

Because the linear operator involves fourth and second derivatives, solving for $u^{n+1}$ requires inverting a linear system in Fourier space.  
We start from the initial concentration $u^0$ and apply this step repeatedly: for $n = 0, 1, \dots, N-1$ we compute $u^{n+1}$ from $u^n$ using the backward Euler IMEX rule.  
This produces a sequence $\{u^n\}_{n=0}^N$ that approximates the evolution of the concentration field.

### Song IMEX Runge–Kutta Scheme

In addition to backward Euler, a three–stage IMEX Runge–Kutta scheme proposed by Song is implemented. The scheme advances the solution using a combination of implicit treatment of the linear stiff terms and explicit treatment of the nonlinear term. Different coefficient sets are tested and compared in terms of stability and accuracy.

### Spatial Discretization

All spatial derivatives are approximated using Fourier spectral methods. The solution is represented on a uniform grid, and derivatives are computed using fast Fourier transforms (FFTs). Periodic boundary conditions are assumed in both spatial directions.

### Manufactured Solutions and Convergence

To verify the implementation, the method of manufactured solutions is used. An analytical solution $u(x,y,t)$ is prescribed, and the corresponding source term $g(x,y,t)$ is computed symbolically. Convergence studies in time are then performed while keeping the spatial resolution fixed.

### Diagnostics

The following physical quantities are monitored during the simulations:
- Total mass
- Mixing energy
- Interfacial energy
- Total free energy

These quantities are used to verify mass conservation and energy dissipation properties of the numerical schemes.

### Numerical Experiments

The notebook includes numerical experiments demonstrating:
- Time convergence of the backward Euler and IMEX schemes
- Comparison of different IMEX coefficient sets
- Spinodal decomposition from random initial data
- Long–time coarsening and Ostwald ripening
- Mass conservation and energy decay

Animations of the solution evolution are generated for selected experiments.