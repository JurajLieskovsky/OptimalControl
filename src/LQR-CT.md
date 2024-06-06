# Continuous-Time Linear-Quadratic Regulator

For a linear time-invariant continuous-time system
$$
\dot{\bm{x}}(t) = \underbrace{\bm{A} \bm{x}(t) + \bm{B} \bm{u}(t)}_{\bm{f}(\bm{x}(t), \bm{u}(t))}
$$
and a quadratic total cost
$$
J(\bm{x}(t_0),\bm{u}(\tau),t_0,t_f) = \underbrace{\bm{x}(t_f)^\top \bm{Q} \, \bm{x}(t_f)}_{\Phi(\bm{x}_N)} + \int_{t_0}^{t_f} \underbrace{\bm{x}(\tau)^\top \bm{Q} \, \bm{x}(\tau) + \bm{u}(\tau)^\top \bm{R} \, \bm{u}(\tau)}_{\mathcal{L}(\bm{x}(\tau), \bm{u}(\tau))} \, d\tau,
$$
where $\bm{Q} \succeq 0$ and $\bm{R} \succ 0$, of its trajectory $\bm{x}(\tau)$, $\tau \in (t_0,t_f\rangle$, it is known that the value function takes a quadratic form
$$
V(\bm{x}(t),t,t_f) = \bm{x}(t)^\top \bm{S}(t) \, \bm{x}(t), \quad \bm{S}(t) \succ 0.
$$
When substituted into the [Hamilton-Jacobi-Bellman Equation](HJB.md) along with the system's dynamics we attain
$$
-\bm{x}^\top \dot{\bm{S}}(t) \, \bm{x} = \min_{\bm{u}} \left(\bm{x}^\top \bm{Q} \, \bm{x} + \bm{u}^\top \bm{R} \, \bm{u} + 2 \, \bm{x}^\top \bm{S}(t) \left(\bm{A} \, \bm{x} + \bm{B} \, \bm{u}\right) \right), \ \bm{x} = \bm{x}(t), \bm{u} = \bm{u}(t) . \tag{1}
$$
To find the minimum, we may take the gradient of its argument (which is by design quadratic and convex) with respect to $\bm{u}(t)$, set it to zero and find the solution (optimal control input)
$$
\bm{u}^*(t) = -\bm{R}^{-1} \bm{B}^\top \bm{S}(t) \, \bm{x}(t) .
$$

The input can then be substituted back into (1). As the equation must hold for all $\bm{x}(t)$, through basic manipulations we then attain the *continuous-time differential Riccati equation (CDRE)*
$$
-\dot{\bm{S}}(t) = \bm{Q} - \bm{S}(t) \bm{B}^\top \bm{R}^{-1} \bm{B} \bm{S}(t) + \bm{S}(t) \bm{A} + \bm{A}^\top \bm{S}(t), \quad \bm{S}(t_f) = \bm{Q}
$$
for a finite horizon $t_f \in \mathbb{R}$. For the infinite horizon LQR where $t_f = \infty$ the solution is given by the (positive-definite) fixed point of this equation:
$$
\bm{0} = \bm{Q} - \bm{S} \bm{B}^\top \bm{R}^{-1} \bm{B} \bm{S} + \bm{S} \bm{A} + \bm{A}^\top \bm{S}, \quad \bm{S} = \bm{S}^T \succ \bm{0},
$$
known as the *continuous-time algebraic Riccati equation (CARE)* @@Underactuated2023[^1].

---

[^1]: Follows mostly section 8.2.1 but also leads to the result of 8.1, borrowing some elements.

