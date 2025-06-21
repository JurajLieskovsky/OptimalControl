# Discrete-Time Finite-horizon Linear-Quadratic Regulator

For a linear time-variant discrete-time system
$$
x_{k+1} = \underbrace{A_k x_k + B_k u_k}_{f(x_k, u_k, k)}
$$
and a quadratic total cost
$$
J(x_0,u_{0:N-1},0) = \underbrace{x_N^\top \, Q_N \, x_N}_{\Phi(x_N)} + \sum_{i=0}^{N-1} \underbrace{x_i^\top Q \, x_i + u_i^\top R \, u_i}_{l(x_i, u_i, i)}
, \quad Q_N \succeq 0, \; Q \succeq 0, \; R \succ 0
$$
of its trajectory $(x_{0:N}, u_{0:N-1})$ the optimal controller can be derived based on the assumption that the value function takes the form
$$
V(x_k,k) = x_k^\top S_k x_k, \quad S_k \succ 0.
$$
When substituted into the [Bellman Equation](BellmanEqn.md) along with the system's dynamics we attain
$$
x_k^\top S_k x_k = \min_{u_k} \left\{x_k^\top Q x_k + u_k^\top R u_k + (A_k x_k + B_k u_k)^\top S_{k+1} (A_k x_k + B_k u_k)\right\} \tag{1}.
$$
To find the minimum, we may take the gradient of its argument (which is by design quadratic and convex) with respect to $u_k$, set it to zero and find the solution (optimal control input)
$$
u_k^* = - \left(R + B_k^\top S_{k+1} B_k\right)^{-1} B_k^\top S_{k+1} A_k \, x_k.
$$

The input can then be substitued back into (1). As the equation must hold for all $x_k$, through basic manipulations we then attain the *discrete-time dynamic Riccati equation (DDRE)*
$$
S_k = Q + A_k^\top S_{k+1} A_k - A_k^\top S_{k+1} B_k \left(B_k^\top S_{k+1} B_k + R\right)^{-1} B_k^\top S_{k+1} A_k, \quad S_N = Q_N
$$
for a finite horizon $N \in \mathbb{N}$.

