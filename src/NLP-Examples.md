# NLP Problem Examples
## Proportions of a canister
We are tasked with designing the proportions of a 0.5 liter cylindrical canister to minimize its surface area and therefore the amount of material used.

Cylinder's volume and surface are
$$
\begin{aligned}
	V &= \pi r^2 h \\
	S &= 2 \pi (r^2 + rh) \,.
\end{aligned}
$$

### Mathematical model
$$
\begin{aligned}
	\min_{r,h} & \quad 2 \pi (r^2 + rh) \\
	\text{s.t.} & \quad \pi r^2 h = 0.5\\
							& \quad r \geq 0 \\
							& \quad h \geq 0 
\end{aligned}
$$

As we are dealing with a quadratic objective function and a cubic equality constraint, the python package CVXPY does not have an interface to a suitable solver. Fortunately, the julia package JuMP does.

- [julia - JuMP](https://github.com/lieskjur/nmoc-julia/blob/main/src/canister-proportions.jl)

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

### QP-like form
$$
\begin{aligned}
	\bm{Q} &= \begin{bmatrix} 0 & -1 \\ -1 & 0 \end{bmatrix} \\
	\bm{c} &= \begin{bmatrix} 0 \\ 0 \end{bmatrix} \\ 
	\bm{A} &= \begin{bmatrix} 2 & 2 \end{bmatrix} \\ 
	\bm{b} &= \begin{bmatrix} 100 \end{bmatrix} \\ 
\end{aligned}
$$

The reason why this problem falls under nonlinear programming is that Q is not positive semi-definite and therefore the problem is non-convex.

### Code
- [julia - JuMP](https://github.com/lieskjur/nmoc-julia/blob/main/src/rectangular_plot_dimensions.jl)

