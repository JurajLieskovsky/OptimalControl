# Direct LQ MPC Examples

## 2-DOF double integrator

Let control a 2-DOF double integrator with an MPC controller with a prediction horizon of one second and quadratic running cost penalizing the state-error and input level.

We will use the first order approximation
$$
\bm{x}_{k+1} = \underbrace{(\bm{I} + \bm{A}_c h)}_{\bm{A}} \bm{x}_k + \underbrace{\bm{B}_c h}_{\bm{B}} \, \bm{u}_k 
$$
with a timestep of $10^{-2}$s to discretize its continuous dynamics
$$
\dot{\bm{x}} = \bm{f}(\bm{x},\bm{u}) =
\underbrace{\begin{bmatrix}
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1 \\
0 & 0 & 0 & 0 \\
0 & 0 & 0 & 0
\end{bmatrix}}_{\bm{A}_c}
\bm{x}
+
\underbrace{\begin{bmatrix}
0 & 0 \\
0 & 0 \\
1 & 0 \\
0 & 1 \\
\end{bmatrix}}_{\bm{B}_c}
\bm{u}
\,.
$$

We will formulate the running cost as
$$
l(\bm{x}_k,\bm{u}_k) = \bm{x}_k^\top \bm{Q} \, \bm{x}_k + \bm{u}_k^\top \bm{R} \, \bm{u}_k
$$
and place additional constraints
$$
-2 \leq \bm{u}_k \leq 2
$$
on the controllers inputs.


### Code
- Direct
	- julia
		- [JuMP](https://github.com/lieskjur/nmoc-julia/blob/main/src/MPC-JuMP.jl)
		- [OSQP](https://github.com/lieskjur/nmoc-julia/blob/main/src/MPC-OSQP.jl)
	- python
		- [CVXPY](https://github.com/lieskjur/nmoc-python/blob/main/src/MPC-CVXPY.py)
		- [OSQP](https://github.com/lieskjur/nmoc-python/blob/main/src/MPC-OSQP.py)

