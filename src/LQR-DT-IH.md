# Discrete-Time Infinite-horizon Linear-Quadratic Regulator

For a linear time-invariant discrete-time system
$$
x_{k+1} = \underbrace{A x_k + B u_k}_{f(x_k, u_k, k)}
$$
and a quadratic total cost
$$
J(x_0,u_{0:\infty},0) = \sum_{i=0}^{\infty} \underbrace{x_i^\top Q \, x_i + u_i^\top R \, u_i}_{l(x_i, u_i, i)}
, \quad Q \succeq 0, \; R \succ 0
$$
of its trajectory $(x_{0:\infty}, u_{0:\infty})$ the optimal controller can be derived based on the assumption that the value function on the infinite horizon takes the time-invariant form
$$
V(x_k,k) = x_k^\top P \, x_k, \quad P \succ 0.
$$

When substituted into the [Bellman Equation](BellmanEqn.md) along with the system's dynamics we attain
$$
x_k^\top P \, x_k = \min_{u_k} \left\{x_k^\top Q \, x_k + u_k^\top R \, u_k + (A x_k + B u_k)^\top P (A x_k + B u_k)\right\} \tag{1}.
$$
To find the minimum, we may take the gradient of its argument (which is by design quadratic and convex) with respect to $u_k$, set it to zero and find the solution (optimal control input)
$$
u_k^* = - \left(R + B^\top P \, B\right)^{-1} B^\top P A \, x_k .
$$

The input can then be substituted back into (1). As the equation must hold for all $x_k$, through basic manipulations we then attain the *discrete-time algebraic Riccati equation (DARE)*
$$
P = Q + A^\top P A - A^\top P \, B \left(B^\top P B + R\right)^{-1} B^\top P A, \quad P \succ 0.
$$
