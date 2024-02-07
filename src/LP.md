# Linear Programming

Let us consider a constrained optimization problem in the form
$$
\begin{aligned}
	\max_x & \quad c^\top x \\
	\text{s.t.} & \quad A x \leq b \\
	            & \quad x \geq 0 \,.
\end{aligned}
$$

As both the objective function and constraints are linear the problem is convex. For this reason KKT conditions are not only necessary but also sufficient if a feasible $x$ w.r.t the constraints exists.

## KKT conditions
The KKT conditions of this problem can be states as:
$$
\begin{aligned}
c + A^\top \mu &= 0 & \text{stationarity} \\
A x &\leq b & \text{primal feasibility} \\
x &\geq 0 & \\ 
\mu &\geq 0 & \text{dual feasibility} \\
\mu^\top (A x - b) &= 0 & \text{complementary slackness}
\end{aligned}
$$

## Examples

### Box constrained function

### Data flow
