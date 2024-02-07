# Quadratic Programming

Let us consider a constrained optimization problem in the form
$$
\begin{aligned}
	\min_x & \quad \frac{1}{2} x^\top Q x + c^\top x \\
	\text{s.t.} & \quad A x \leq b \,,
\end{aligned}
$$
where $Q = Q^\top$.

As the objective function is quadratic and the constraints linear the problem is convex. For this reason KKT conditions are not only necessary but also sufficient if a feasible $x$ w.r.t the constraints exists.

## KKT Conditions

The KKT conditions of this problem can be states as:
$$
\begin{aligned}
Q x + c + A^\top \mu &= 0 & \text{stationarity} \\
\quad A x &\leq b & \text{primal feasibility} \\
\mu &\geq 0 & \text{dual feasibility} \\
\mu^\top (A x - b) &= 0 & \text{complementary slackness}
\end{aligned}
$$

## Examples

### Circular paraboloid with a single constraint

Let's visualize and solve a very simple QP problem of minimizing $x$ and $y$ for an objective function in the form of a circular paraboloid and a single linear inequality constraint.

#### Mathematical model
$$
\begin{aligned}
	\min_{x_1, x_2} & \quad x_1^2 + x_2^2 \\
	\text{s.t.} & \quad -2 x_1 + x_2 \leq - 1 
\end{aligned}
$$

#### Canonical form
$$
\begin{aligned}
	Q &= \begin{bmatrix} 2 & 0 \\ 0 & 2 \end{bmatrix} \\
	c &= \begin{bmatrix} 0 \\ 0 \end{bmatrix} \\ 
	A &= \begin{bmatrix} -1 & 1 \end{bmatrix} \\ 
	b &= \begin{bmatrix} -1 \end{bmatrix} \\ 
\end{aligned}
$$

### Tree nursery
We are tasked with planting a new patch of forest to offset logging activity. Because of the wildlife living there, the young trees need to be fences off from the rest of the forest until they mature.

As we will be planting adjacent plots in the future, we have decided upon fencing off a rectangular area. The factor limiting its size is that we only have 100 meters of suitable fencing. What is the largest rectangular area that we can plant?

#### Mathematical model
$$
\begin{aligned}
	\max_{x_1, x_2} & \quad x_1 x_2 \\
	\text{s.t.} & \quad 2x_1 + 2x_2 \leq 100 
\end{aligned}
$$

#### Canonical form
$$
\begin{aligned}
	Q &= \begin{bmatrix} 0 & 1 \\ 1 & 0 \end{bmatrix} \\
	c &= \begin{bmatrix} 0 \\ 0 \end{bmatrix} \\ 
	A &= \begin{bmatrix} 2 & 2 \end{bmatrix} \\ 
	b &= \begin{bmatrix} 100 \end{bmatrix} \\ 
\end{aligned}
$$

### Cable driven manipulator
