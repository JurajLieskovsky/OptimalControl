# Continuous-Time Linear-Quadratic Regulator

For a linear time-invariant continuous-time system
$$
\dot{x}(t) = \underbrace{A x(t) + B u(t)}_{f(x(t), u(t), t)}
$$
and a quadratic total cost
$$
J(x(t_0),u(\tau),t_0) = \underbrace{x(t_f)^\top Q \, x(t_f)}_{\Phi(x_N)} + \int_{t_0}^{t_f} \underbrace{x(\tau)^\top Q \, x(\tau) + u(\tau)^\top R \, u(\tau)}_{l(x(\tau), u(\tau), \tau)} \, d\tau,
$$
where $Q \succeq 0$ and $R \succ 0$, of its trajectory $x(\tau)$, $\tau \in (t_0,t_f\rangle$, it is known that the value function takes a quadratic form
$$
V(x(t),t) = x(t)^\top S(t) \, x(t), \quad S(t) \succ 0.
$$
When substituted into the [Hamilton-Jacobi-Bellman Equation](HJB.md) along with the system's dynamics we attain
$$
-x(t)^\top \dot{S}(t) \, x(t) = \min_{u(t)} \left\{x(t)^\top Q \, x(t) + u(t)^\top R \, u(t) + 2 \, x(t)^\top S(t) \left(A \, x(t) + B \, u(t)\right) \right\}. \tag{1}
$$
To find the minimum, we may take the gradient of its argument (which is by design quadratic and convex) with respect to $u(t)$, set it to zero and find the solution (optimal control input)
$$
u^*(t) = -R^{-1} B^\top S(t) \, x(t) .
$$

The input can then be substituted back into (1). As the equation must hold for all $x(t)$, through basic manipulations we then attain the *continuous-time differential Riccati equation (CDRE)*
$$
-\dot{S}(t) = Q - S(t) B^\top R^{-1} B S(t) + S(t) A + A^\top S(t), \quad S(t_f) = Q
$$
for a finite horizon $t_f \in \mathbb{R}$. For the infinite horizon LQR where $t_f = \infty$ the solution is given by the (positive-definite) fixed point of this equation:
$$
0 = Q - S B^\top R^{-1} B S + S A + A^\top S, \quad S = S^T \succ 0,
$$
known as the *continuous-time algebraic Riccati equation (CARE)* @@Underactuated2023[^1].

---

[^1]: Follows mostly section 8.2.1 but also leads to the result of 8.1, borrowing some elements.

