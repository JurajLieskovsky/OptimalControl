# Discrete-Time Linear-Quadratic Regulator

## Infinite horizon

For a linear time-invariant discrete-time system
$$
x_{k+1} = \underbrace{A x_k + B u_k}_{f(x_k, u_k, k)}
$$
and a quadratic total cost
$$
J(x_0,\{u_i\}_{i=0}^{\infty},0) = \sum_{i=0}^{\infty} \underbrace{x_i^\top Q x_i + u_i^\top R u_i}_{l(x_i, u_i, i)}
, \quad Q \succeq 0, \; R \succ 0
$$
of its trajectory $\{x_i\}_{i=0}^\infty$ the optimal controller can be derived based on the assumption that the value function on the infinite horizon takes the time-invariant form
$$
V(x_k,k) = x_k^\top S x_k, \quad S \succ 0.
$$

When substituted into the [Bellman Equation](BellmanEqn.md) along with the system's dynamics we attain
$$
x_k^\top S x_k = \min_{u_k} \left\{x_k^\top Q x_k + u_k^\top R u_k + (A x_k + B u_k)^\top S (A x_k + B u_k)\right\} \tag{1}.
$$
To find the minimum, we may take the gradient of its argument (which is by design quadratic and convex) with respect to $u_k$, set it to zero and find the solution (optimal control input)
$$
u_k^* = - \left(R + B^\top S B\right)^{-1} B^\top S A x_k .
$$

The input can then be substitued back into (1). As the equation must hold for all $x_k$, through basic manipulations we then attain the *discrete-time algebraic Riccati equation (DARE)*
$$
S = Q + A^\top S A - A^\top S B \left(B^\top S B + R\right)^{-1} B^\top S A, \quad S \succ 0.
$$

## Finite horizon

For a linear time-invariant discrete-time system
$$
x_{k+1} = \underbrace{A x_k + B u_k}_{f(x_k, u_k, k)}
$$
and a quadratic total cost
$$
J(x_0,\{u_i\}_{i=0}^{N},0) = \underbrace{x_N^\top Q_N x_N}_{\Phi(x_N)} + \sum_{i=0}^{N-1} \underbrace{x_i^\top Q x_i + u_i^\top R u_i}_{l(x_i, u_i, i)}
, \quad Q_N \succeq 0, \; Q \succeq 0, \; R \succ 0
$$
of its trajectory $\{x_i\}_{i=0}^N$ the optimal controller can be derived based on the assumption that the value function takes the form
$$
V(x_k,k) = x_k^\top S_k x_k, \quad S_k \succ 0.
$$
When substituted into the [Bellman Equation](BellmanEqn.md) along with the system's dynamics we attain
$$
x_k^\top S_k x_k = \min_{u_k} \left\{x_k^\top Q x_k + u_k^\top R u_k + (A x_k + B u_k)^\top S_{k+1} (A x_k + B u_k)\right\} \tag{1}.
$$
To find the minimum, we may take the gradient of its argument (which is by design quadratic and convex) with respect to $u_k$, set it to zero and find the solution (optimal control input)
$$
u_k^* = - \left(R + B^\top S_{k+1} B\right)^{-1} B^\top S_{k+1} A x_k .
$$

The input can then be substitued back into (1). As the equation must hold for all $x_k$, through basic manipulations we then attain the *discrete-time dynamic Riccati equation (DDRE)*
$$
S_k = Q + A^\top S_{k+1} A - A^\top S_{k+1} B \left(B^\top S_{k+1} B + R\right)^{-1} B^\top S_{k+1} A, \quad S_N = Q_N
$$
for a finite horizon $N \in \mathbb{N}$.

