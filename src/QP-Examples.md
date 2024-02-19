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

## Tree nursery
We are tasked with planting a new patch of forest to offset logging activity. Because of the wildlife living there, the young trees need to be fences off from the rest of the forest until they mature.

As we will be planting adjacent plots in the future, we have decided upon fencing off a rectangular area. The factor limiting its size is that we only have 100 meters of suitable fencing. What is the largest rectangular area that we can plant?

### Mathematical model
$$
\begin{aligned}
	\max_{x_1, x_2} & \quad x_1 x_2 \\
	\text{s.t.} & \quad 2x_1 + 2x_2 \leq 100 
\end{aligned}
$$

### Canonical form
$$
\begin{aligned}
	\bm{Q} &= \begin{bmatrix} 0 & 1 \\ 1 & 0 \end{bmatrix} \\
	\bm{c} &= \begin{bmatrix} 0 \\ 0 \end{bmatrix} \\ 
	\bm{A} &= \begin{bmatrix} 2 & 2 \end{bmatrix} \\ 
	\bm{b} &= \begin{bmatrix} 100 \end{bmatrix} \\ 
\end{aligned}
$$

### Code
- [julia - JuMP](https://github.com/lieskjur/nmoc-julia/blob/main/src/rectangular_plot_dimensions.jl)

## Model Predictive Control (MPC)

Optimal control of linear systems on a finite horizon can be more often than not stated as a QP. Formulation of these problems is a topic of future chapters.
