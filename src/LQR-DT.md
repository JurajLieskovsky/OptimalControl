# Discrete-Time Linear-Quadratic Regulator

For a linear time-invariant discrete-time system
$$
\bm{x}_{k+1} = \underbrace{\bm{A} \bm{x}_k + \bm{B} \bm{u}_k}_{\bm{f}(\bm{x}_k, \bm{u}_k)}
$$
and a quadratic total cost
$$
J(\bm{x}_0,\{\bm{u}_i\}_{i=0}^{N}) = \underbrace{\bm{x}_N^\top \bm{Q} \bm{x}_N}_{\Phi(\bm{x}_N)} + \sum_{i=0}^{N-1} \underbrace{\bm{x}_i^\top \bm{Q} \bm{x}_i + \bm{u}_i^\top \bm{R} \bm{u}_i}_{\mathcal{L}(\bm{x}_i, \bm{u}_i)}
, \quad \bm{Q} \succeq 0, \bm{R} \succ 0
$$
of its trajectory $\{\bm{x}_i\}_{i=0}^N$, it is known that the value function takes a quadratic form
$$
V(\bm{x}_k,k,N) = \bm{x}_k^\top \bm{S}_k \bm{x}_k, \quad \bm{S}_k \succ 0.
$$
When substituted into the [Bellman Equation](BellmanEqn.md) along with the system's dynamics we attain
$$
\bm{x}_k^\top \bm{S}_k \bm{x}_k = \min_{\bm{u}_k} \left(\bm{x}_k^\top \bm{Q} \bm{x}_k + \bm{u}_k^\top \bm{R} \bm{u}_k + (\bm{A} \bm{x}_k + \bm{B} \bm{u}_k)^\top \bm{S}_{k+1} (\bm{A} \bm{x}_k + \bm{B} \bm{u}_k)\right) \tag{1}.
$$
To find the minimum, we may take the gradient of its argument (which is by design quadratic and convex) with respect to $\bm{u}_k$, set it to zero and find the solution (optimal control input)
$$
\bm{u}_k^* = - \left(\bm{R} + \bm{B}^\top \bm{S}_{k+1} \bm{B}\right)^{-1} \bm{B}^\top \bm{S}_{k+1} \bm{A} \bm{x}_k .
$$

The input can then be substitued back into (1). As the equation must hold for all $\bm{x}_k$, through basic manipulations we then attain the *discrete-time dynamic Riccati equation (DDRE)*
$$
\bm{S}_k = \bm{Q} + \bm{A}^\top \bm{S}_{k+1} \bm{A} - \bm{A}^\top \bm{S}_{k+1} \bm{B} \left(\bm{B}^\top \bm{S}_{k+1} \bm{B} + \bm{R}\right)^{-1} \bm{B}^\top \bm{S}_{k+1} \bm{A}, \quad \bm{S}_N = \bm{Q}
$$
for a finite horizon $N \in \mathbb{N}$. For the infinite horizon LQR where $N = \infty$ the solution is given by the (positive-definite) fixed point of this equation:
$$
\bm{S} = \bm{Q} + \bm{A}^\top \bm{S} \bm{A} - \bm{A}^\top \bm{S} \bm{B} \left(\bm{B}^\top \bm{S} \bm{B} + \bm{R}\right)^{-1} \bm{B}^\top \bm{S} \bm{A}, \quad \bm{S} \succ 0,
$$
known as the *discrete-time algebraic Riccati equation (DARE)* @@Underactuated2023[^1].

---

[^1]: Follows section 8.3.1.
