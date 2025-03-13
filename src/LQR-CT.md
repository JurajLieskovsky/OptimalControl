# Continuous-Time Linear-Quadratic Regulator

## Infinite horizon

For a linear time-invariant continuous-time system
$$
\dot{x}(t) = \underbrace{A x(t) + B u(t)}_{f(x(t), u(t), t)}
$$
and a quadratic total cost
$$
J(x(t_0),u(\tau),t_0) = \int_{t_0}^{\infty} \underbrace{x(\tau)^\top Q \, x(\tau) + u(\tau)^\top R \, u(\tau)}_{l(x(\tau), u(\tau), \tau)} \, d\tau,
$$
where $Q \succeq 0$ and $R \succ 0$, of its trajectory $x(\tau)$, $\tau \in (t_0,t_f\rangle$ the optimal controller can be derived based on the assumption that the value function takes the form
$$
V(x(t),t) = x(t)^\top S \, x(t), \quad S \succ 0.
$$
When substituted into the [Hamilton-Jacobi-Bellman Equation](HJB.md) along with the system's dynamics we attain
$$
0 = \min_{u} \left\{x^\top Q \, x + u^\top R \, u + 2 \, x^\top S \left(A \, x + B \, u\right) \right\}, \tag{1}
$$
where $x = x(t)$ and $u = u(t)$. To find the minimum, we may take the gradient of its argument (which is by design quadratic and convex) with respect to $u(t)$, set it to zero and find the solution (optimal control input)
$$
u^*(t) = -R^{-1} B^\top S \, x(t) .
$$

The input can then be substituted back into (1). As the equation must hold for all $x(t)$, through basic manipulations we then attain the *continuous-time algebraic Riccati equation (CARE)*
$$
0 = Q - S B^\top R^{-1} B S + S A + A^\top S, \quad S \succ 0.
$$

## Finite horizon

For a linear time-invariant continuous-time system
$$
\dot{x}(t) = \underbrace{A x(t) + B u(t)}_{f(x(t), u(t), t)}
$$
and a quadratic total cost
$$
J(x(t_0),u(\tau),t_0) = \underbrace{x(t_f)^\top Q_f \, x(t_f)}_{\Phi(x_N)} + \int_{t_0}^{t_f} \underbrace{x(\tau)^\top Q \, x(\tau) + u(\tau)^\top R \, u(\tau)}_{l(x(\tau), u(\tau), \tau)} \, d\tau,
$$
where $Q_f \succeq 0$, $Q \succeq 0$, and $R \succ 0$, of its trajectory $x(\tau)$, $\tau \in (t_0,t_f\rangle$ the optimal controller can be derived based on the assumption that the value function takes the form
$$
V(x(t),t) = x(t)^\top S(t) \, x(t), \quad S(t) \succ 0.
$$
When substituted into the [Hamilton-Jacobi-Bellman Equation](HJB.md) along with the system's dynamics we attain
$$
-x^\top \dot{S} \, x = \min_{u} \left\{x^\top Q \, x + u^\top R \, u + 2 \, x^\top S \left(A \, x + B \, u\right) \right\}, \tag{1}
$$
where $x = x(t)$ and $u = u(t)$. To find the minimum, we may take the gradient of its argument (which is by design quadratic and convex) with respect to $u(t)$, set it to zero and find the solution (optimal control input)
$$
u^*(t) = -R^{-1} B^\top S(t) \, x(t) .
$$

The input can then be substituted back into (1). As the equation must hold for all $x(t)$, through basic manipulations we then attain the *continuous-time differential Riccati equation (CDRE)*
$$
-\dot{S}(t) = Q - S(t) \, B^\top R^{-1} B \, S(t) + S(t) \, A + A^\top \! S(t) 
$$
for a finite horizon $t_f \in \mathbb{R}$. Supplemented with the boundary conditon $S(t_f) = Q_f$, the CDRE forms a initial value problem (IVP) which can be solved using numerical integration. Numerical errors in the integration process may lead to the loss of positive-semi-definiteness. To overcome this, instead of integrating $S(t)$ directly, we may use its factorized form $S(t) = P(t) \, P^\top\!(t)$ a.k.a. the square-root form where
$$
-\dot{P}(t) = \frac{1}{2} Q \, {P^{-\top}\!(t)} - \frac{1}{2} {S(t)} \, B \, R^{-1} B^\top \! {P(t)} + A^\top \! {P(t)}.
$$
As $P(t)$ must be invertible $Q_f$ must be (numerically) positive definite. Consequenlty we may use the cholesky factorization in order to form the boundary condition
$$
P(t_f) = L, \quad Q_f = L \, L^\top
$$
