# Discrete-Time Linear-Quadratic Regulator

For a linear time-invariant discrete-time system
$$
x_{k+1} = \underbrace{A x_k + B u_k}_{f(x_k, u_k, k)}
$$
and a quadratic total cost
$$
J(x_0,\{u_i\}_{i=0}^{N},0) = \underbrace{x_N^\top Q x_N}_{\Phi(x_N)} + \sum_{i=0}^{N-1} \underbrace{x_i^\top Q x_i + u_i^\top R u_i}_{l(x_i, u_i, i)}
, \quad Q \succeq 0, R \succ 0
$$
of its trajectory $\{x_i\}_{i=0}^N$, it is known that the value function takes a quadratic form
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
S_k = Q + A^\top S_{k+1} A - A^\top S_{k+1} B \left(B^\top S_{k+1} B + R\right)^{-1} B^\top S_{k+1} A, \quad S_N = Q
$$
for a finite horizon $N \in \mathbb{N}$. For the infinite horizon LQR where $N = \infty$ the solution is given by the (positive-definite) fixed point of this equation:
$$
S = Q + A^\top S A - A^\top S B \left(B^\top S B + R\right)^{-1} B^\top S A, \quad S \succ 0,
$$
known as the *discrete-time algebraic Riccati equation (DARE)* @@Underactuated2023[^1].

---

[^1]: Follows section 8.3.1.
