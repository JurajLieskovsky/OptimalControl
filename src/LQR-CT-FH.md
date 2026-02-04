# Continuous-Time Infinite-Horizon Linear-Quadratic Regulator

For a linear time-variant continuous-time system
$$
\dot{x}(t) = \underbrace{A(t) x(t) + B(t) u(t)}_{f(x(t), u(t), t)}
$$
and a quadratic total cost
$$
J(x(t_0),u(\tau),t_0) = \underbrace{x(t_f)^\top Q_f \, x(t_f)}_{\Phi(x_N)} + \int_{t_0}^{t_f} \underbrace{x(\tau)^\top Q \, x(\tau) + u(\tau)^\top R \, u(\tau)}_{l(x(\tau), u(\tau), \tau)} \, d\tau,
$$
where $Q_f \succeq 0$, $Q \succeq 0$, and $R \succ 0$, of its trajectory $(x(\tau), u(\tau))$, $\tau \in \langle t_0,t_f\rangle$ the optimal controller can be derived based on the assumption that the value function takes the form
$$
V(x(t),t) = x(t)^\top P(t) \, x(t), \quad P(t) \succ 0.
$$
When substituted into the [Hamilton-Jacobi-Bellman Equation](HJB.md) along with the system's dynamics we attain
$$
\begin{gathered}
-x(t)^\top\! \dot{P}(t)\, x(t) = \\
\min_{u(t)} \left\{x(t)^\top Q \, x(t) + u(t)^\top R \, u(t) + 2 \, x(t)^\top P(t) \left(A(t) \, x(t) + B(t) \, u(t) \right) \right\}. \tag{1}
\end{gathered}
$$
To find the minimum, we may take the gradient of its argument (which is by design quadratic and convex) with respect to $u(t)$, set it to zero and find the solution (optimal control input)
$$
u^*(t) = -R^{-1} B(t)^\top P(t) \, x(t) .
$$

The input can then be substituted back into (1). As the equation must hold for all $x(t)$, through basic manipulations we then attain the *differential Riccati equation (DRE)*
$$
-\dot{P}(t) = Q - P(t) \, B(t)^\top R^{-1} B(t) \, P(t) + P(t) \, A(t) + A(t)^\top \! P(t) 
$$
for a finite horizon $t_f \in \mathbb{R}$. Supplemented with the boundary conditon $P(t_f) = Q_f$, the DRE forms an initial value problem (IVP) which can be solved using numerical integration. However, solving the problem is not straght-forward. The positive semi-definiteness of $P(t)$ is a property that is not inherently preserved by all integration methods. This necessitates the use of either symplectic integration methods (often tailored for DREs) or factorizing $P(t)$.
