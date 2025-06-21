# Continuous-Time Infinite-Horizon Linear-Quadratic Regulator

For a linear time-invariant continuous-time system
$$
\dot{x}(t) = \underbrace{A x(t) + B u(t)}_{f(x(t), u(t), t)}
$$
and a quadratic total cost
$$
J(x(t_0),u(\tau),t_0) = \int_{t_0}^{\infty} \underbrace{x(\tau)^\top Q \, x(\tau) + u(\tau)^\top R \, u(\tau)}_{l(x(\tau), u(\tau), \tau)} \, d\tau,
$$
where $Q \succeq 0$ and $R \succ 0$, of its trajectory $(x(\tau), u(\tau))$, $\tau \in (t_0,\infty)$ the optimal controller can be derived based on the assumption that the value function takes the form
$$
V(x(t),t) = x(t)^\top S \, x(t), \quad S \succ 0.
$$
When substituted into the [Hamilton-Jacobi-Bellman Equation](HJB.md) along with the system's dynamics we attain
$$
0 = \min_{u(t)} \left\{x(t)^\top Q \, x(t) + u(t)^\top R \, u(t) + 2 \, x(t)^\top S \left(A \, x(t) + B \, u(t)\right) \right\}. \tag{1}
$$
To find the minimum, we may take the gradient of its argument (which is by design quadratic and convex) with respect to $u(t)$, set it to zero and find the solution (optimal control input)
$$
u^*(t) = -R^{-1} B^\top S \, x(t) .
$$

The input can then be substituted back into (1). As the equation must hold for all $x(t)$, through basic manipulations we then attain the *continuous-time algebraic Riccati equation (CARE)*
$$
0 = Q - S B^\top R^{-1} B S + S A + A^\top S, \quad S \succ 0.
$$
