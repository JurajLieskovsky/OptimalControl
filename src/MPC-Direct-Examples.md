# Direct LQ MPC Examples

## 2-DOF double integrator

Let control a 2-DOF double integrator with an MPC controller with a prediction horizon of one second and quadratic running cost penalizing the state-error and input level.

We will use the first order approximation
$$
x_{k+1} = (I + Ah) x + Bh u 
$$
with a timestep of $10^{-2}$s to discretize its continuous dynamics
$$
\dot{x} = f(x,u) =
\begin{bmatrix}
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1 \\
0 & 0 & 0 & 0 \\
0 & 0 & 0 & 0
\end{bmatrix}
x
+
\begin{bmatrix}
0 & 0 \\
0 & 0 \\
1 & 0 \\
0 & 1 \\
\end{bmatrix}
u
\,.
$$

We will formulate the running cost as
$$
l(x_k,u_k) = x_k^\top Q x_k + u_k^\top R u_k
$$
and additionally place the constraints
$$
-2 \leq u_k \leq 2
$$
on the controllers inputs.


### Code
- julia
	- [JuMP](https://github.com/lieskjur/nmoc-julia/blob/main/src/MPC-JuMP.jl)
	- [OSQP](https://github.com/lieskjur/nmoc-julia/blob/main/src/MPC-OSQP.jl)
- python
	- [CVXPY](https://github.com/lieskjur/nmoc-python/blob/main/src/MPC-CVXPY.py)
	- [OSQP](https://github.com/lieskjur/nmoc-python/blob/main/src/MPC-OSQP.py)

