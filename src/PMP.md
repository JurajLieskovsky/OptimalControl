# Pontryagin's Maximum/Minimum Principle

Pontyagin's maximum/minimum principle is an alternative to the Bellman principle for continuous-time systems. It is derived from Hamilton's equations which can also be used to represent the equations of motion of an uncontrolled system.

Let us consider the optimal control problem
$$
\begin{aligned}
\min &\quad \Phi(\bm{x}(t_f)) + \int_{t_0}^{t_f} l(\bm{x}(t),\bm{u}(t),t) \, dt \\
\mathrm{s.t.} &\quad \dot{\bm{x}}(t) = \bm{f}(\bm{x}(t),\bm{u}(t),t) ,\quad \forall \bm{x}(t) \in \langle t_0, t_f\rangle, \\
&\quad \bm{x}(t_0) = \tilde{\bm{x}}_0.
\end{aligned}
$$
The Lagrangian of the problem takes the form
$$
\mathcal{L}(\dot{\bm{x}},\bm{x},\bm{u},\bm{\lambda},t) = l(\bm{x},\bm{u},t) + \bm{\lambda}^\top \left(\dot{\bm{x}} - \bm{f}(\bm{x},\bm{u},t)\right).
$$ 
When substituted into the Hamiltonian ([Hamilton's equations](HamiltonsEquations.md)), simplifications yield
$$
H(t,\bm{x},\bm{u},\bm{\lambda}) = - l(\bm{x},\bm{u},t) + \bm{\lambda}^\top \bm{f}(\bm{x},\bm{u},t),
$$
where $\bm{u}$ takes over the role of $\bm{y}^\prime$ from the calculus of variations[^1]. An optimal control policy $\bm{u}^*(t)$ is then regarded as
$$
\bm{u}^*(t) = \argmax_{\bm{u}} \ H(t,\bm{x}^*,\bm{u},\bm{\lambda}^*), \quad \forall t \in \langle t_0, t_f\rangle.
$$

## Pontryagin's maximum principle

Pontryagin's maximum principle state's that for
$$
\bm{u}^*(t) = \argmax_{\bm{u}} \ H(t,\bm{x}^*,\bm{u},\bm{\lambda}^*), \quad \forall t \in \langle t_0, t_f\rangle,
$$
the system's state $\bm{x}(t)$ and costate $\bm{\lambda}(t)$ must satisfy [Hamilton's canonical equations](HamiltonsEquations.html#extremization-with-respect-to-y-and-p)
$$
\begin{aligned}
\dot{\bm{x}} &= H_{\bm{\lambda}}, \\
-\dot{\bm{\lambda}} &= H_{\bm{x}},
\end{aligned}
$$
as well as boundary conditions
$$
\begin{aligned}
\bm{x}(t_0) &= \tilde{\bm{x}}_0, \\
\bm{\lambda}(t_f) &= \Phi_{\bm{x}}(\bm{x}(t_f))
\end{aligned}
$$
along an optimal trajectory.

## Pontryagin's minimum principle

In control theory literature, the Hamiltonian is often defined as
$$
H(t,\bm{x},\bm{u},\bm{\lambda}) = l(\bm{x},\bm{u},t) + \bm{\lambda}(t)^\top \bm{f}(\bm{x},\bm{u},t)
$$
which turns the maximization into minimization
$$
\bm{u}^*(t) = \argmin_{\bm{u}} \  H(t,\bm{x}^*,\bm{u},\bm{\lambda}^*), \quad \forall t \in \langle t_0, t_f\rangle,
$$
with the Hamilton's canonical equations and boundary conditions remaining unchanged.


---

[^1]: As is mentioned in the [lecture](https://www.youtube.com/watch?v=Bxc4iy2xUjc&ab_channel=aa4cc) the reasoning is not straight-forward for system's where $\dot{\bm{x}} = \bm{f}(\bm{x},\bm{u},t)$ unlike for simple integrators $\dot{\bm{x}} = \bm{u}$.
