# Quadratic Programming

Let us consider a constrained optimization problem in the form
$$
\begin{aligned}
	\min_{\bm{x}} & \quad \frac{1}{2} \bm{x}^\top \bm{Q} \bm{x} + \bm{c}^\top \bm{x} \\
	\text{s.t.} & \quad \bm{A} \bm{x} \leq \bm{b} \,,
\end{aligned}
$$
where $\bm{Q} = \bm{Q}^\top$.

As the objective function is quadratic and the constraints linear the problem is convex. For this reason KKT conditions are not only necessary but also sufficient if a feasible $x$ w.r.t the constraints exists.

## KKT Conditions

The KKT conditions of this problem can be states as:
$$
\begin{aligned}
\bm{Q} \bm{x} + \bm{c} + \bm{A}^\top \bm{\mu} &= \bm{0} & \text{stationarity} \\
\quad \bm{A} \bm{x} &\leq \bm{b} & \text{primal feasibility} \\
\bm{\mu} &\geq \bm{0} & \text{dual feasibility} \\
\bm{\mu}^\top (\bm{A} \bm{x} - \bm{b}) &= \bm{0} & \text{complementary slackness}
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
	\bm{Q} &= \begin{bmatrix} 2 & 0 \\ 0 & 2 \end{bmatrix} \\
	\bm{c} &= \begin{bmatrix} 0 \\ 0 \end{bmatrix} \\ 
	\bm{A} &= \begin{bmatrix} -1 & 1 \end{bmatrix} \\ 
	\bm{b} &= \begin{bmatrix} -1 \end{bmatrix} \\ 
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
	\bm{Q} &= \begin{bmatrix} 0 & 1 \\ 1 & 0 \end{bmatrix} \\
	\bm{c} &= \begin{bmatrix} 0 \\ 0 \end{bmatrix} \\ 
	\bm{A} &= \begin{bmatrix} 2 & 2 \end{bmatrix} \\ 
	\bm{b} &= \begin{bmatrix} 100 \end{bmatrix} \\ 
\end{aligned}
$$
