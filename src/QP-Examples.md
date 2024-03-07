# QP Problem Examples

## Circular paraboloid with a single constraint

Let's visualize and solve a very simple QP problem of minimizing $x_1$ and $x_2$ for an objective function in the form of a circular paraboloid and a single linear inequality constraint.

### Mathematical model
$$
\begin{aligned}
	\min_{x_1, x_2} & \quad x_1^2 + x_2^2 \\
	\text{s.t.} & \quad -2 x_1 + x_2 \leq - 1 
\end{aligned}
$$

### Canonical form
$$
\begin{aligned}
	\bm{Q} &= \begin{bmatrix} 2 & 0 \\ 0 & 2 \end{bmatrix} \\
	\bm{c} &= \begin{bmatrix} 0 \\ 0 \end{bmatrix} \\ 
	\bm{A} &= \begin{bmatrix} -1 & 1 \end{bmatrix} \\ 
	\bm{b} &= \begin{bmatrix} -1 \end{bmatrix} \\ 
\end{aligned}
$$

### Code
- julia
	- [JuMP](https://github.com/lieskjur/nmoc-julia/blob/main/src/quadratic_programming-JuMP.jl)
	- [OSQP](https://github.com/lieskjur/nmoc-julia/blob/main/src/quadratic_programming-OSQP.jl)
- python
	- [CVXPY](https://github.com/lieskjur/nmoc-python/blob/main/src/quadratic_programming-CVXPY.py)
	- [OSQP](https://github.com/lieskjur/nmoc-python/blob/main/src/quadratic_programming-OSQP.py)

## Economic dispatch
We have three power plants each producing electricity to satisfy the demand of $P_{\Sigma} = 3000$ MW. Each of the power plants has a minimum and maximum capacity $P_{i_{\min}}$ and $P_{i_{\max}}$ and a quadratic cost model associated with its power output $l_i = a_i + b_i P_i + c_i P_i^2$. The capacity limits and cost coefficients are provided in the table bellow.

| $i$         | $a_i$ | $b_i$ | $c_i$ | $P_{i_{\min}}$    | $P_{i_{\max}}$    |
|-------------|-------|-------|-------|-------------------|-------------------|
| 1           | 20    | 5     | 0.02  | 200               | 1000              |
| 2           | 25    | 4     | 0.015 | 300               | 1500              |
| 3           | 30    | 3     | 0.01  | 100               | 800               |

### Mathematical model
$$
\begin{aligned}
	\min_{\{P_i\}_{i=1}^3} & \quad \sum_{i=1}^{3} a_i + b_i P_i + c_i P_i^2 \\
	\text{s.t.} & \quad \sum_{i=1}^{3} P_i = P_{\Sigma} \\
	            & \quad P_{i_{\min}} \leq P_i \leq P_{i_{\min}} \,,\quad i = 1, \ldots, 3\\
\end{aligned}
$$

### OSQP form

$$
\begin{aligned}
	\bm{P} &= \begin{bmatrix} c_1 & 0 & 0 \\ 0 & c_2 & 0 \\ 0 & 0 & c_3 \end{bmatrix} \\
	\bm{q} &= \begin{bmatrix} b_1 \\ b_2 \\ b_3 \end{bmatrix} \\ 
	\bm{A} &= \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \\ 1 & 1 & 1 \end{bmatrix} \\ 
	\bm{l} &= \begin{bmatrix} P_{1_{\min}} \\ P_{2_{\min}} \\ P_{3_{\min}} \\ P_{\Sigma} \end{bmatrix} \\ 
	\bm{u} &= \begin{bmatrix} P_{1_{\max}} \\ P_{2_{\max}} \\ P_{3_{\max}} \\ P_{\Sigma} \end{bmatrix} \\ 
\end{aligned}
$$

### Code
- [python - OSQP](https://github.com/lieskjur/nmoc-python/blob/main/src/economic_dispatch.py)

## Model Predictive Control (MPC)

Optimal control of linear systems on a finite horizon can be more often than not stated as a QP. Formulation of these problems is a topic of future chapters.
