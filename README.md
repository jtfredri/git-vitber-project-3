### Numerical solution of the 2D Cahn–Hilliard equation

This notebook contains numerical solvers for the two–dimensional Cahn–Hilliard equation using **Fourier spectral methods** in space and **implicit–explicit (IMEX)** time discretizations.  
The implementation includes verification via the **method of manufactured solutions**, **convergence studies**, and physical diagnostics such as **mass conservation** and **energy decay**.

---

## The Cahn–Hilliard equation

We consider the Cahn–Hilliard equation on a periodic domain

$$
\Omega = [0,L_x)\times[0,L_y)
$$

The governing PDE is

$$
\partial_t u + \kappa \Delta^2 u - a \Delta u
=
\Delta\!\left(u^3 - (1+a)u\right) + g(x,y,t),
$$

where:

- $(u(x,y,t))$ is the concentration field,
- $(\kappa > 0)$ is the interface parameter,
- $(a \ge 0)$ is a splitting parameter,
- $(g(x,y,t))$ is a prescribed source term.

---

## Backward Euler IMEX scheme

Let $(\tau)$ denote the time step size and define the time grid

$$
t_n = t_0 + n\tau .
$$

The backward Euler IMEX discretization computes $(u^{n+1})$ from $(u^n)$ using

$$
\frac{u^{n+1} - u^n}{\tau}
+ \kappa \Delta^2 u^{n+1}
- a \Delta u^{n+1}
- g^{n+1}
=
\Delta\!\left((u^n)^3 - (1+a)u^n\right).
$$

The linear terms are treated implicitly, while the nonlinear term is treated explicitly.


---

### Song IMEX Runge–Kutta scheme

In addition to backward Euler, a **three–stage IMEX Runge–Kutta scheme** proposed by **Song** is implemented.  
The scheme advances the solution using a combination of:
- **implicit** treatment of the linear stiff terms, and
- **explicit** treatment of the nonlinear term.

Different coefficient sets are tested and compared in terms of **stability** and **accuracy**.