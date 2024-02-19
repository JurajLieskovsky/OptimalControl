# Linear Programming

Let us consider a constrained optimization problem in the form
$$
\begin{aligned}
	\max_{\bm{x}} & \quad \bm{c}^\top \bm{x} \\
	\text{s.t.} & \quad \bm{A} \bm{x} \leq \bm{b} \\
	            & \quad \bm{x} \geq \bm{0} \,.
\end{aligned}
$$

As both the objective function and constraints are linear the problem is convex. For this reason KKT conditions are not only necessary but also sufficient if a feasible $x$ w.r.t the constraints exists.

## KKT conditions
The KKT conditions of this problem can be states as:
$$
\begin{aligned}
\bm{c} + \bm{A}^\top \bm{\mu}_1 - \bm{\mu}_2 &= \bm{0} & \text{stationarity} \\
\bm{A} \bm{x} &\leq \bm{b} & \text{primal feasibility} \\
\bm{x} &\geq \bm{0} & \\ 
\bm{\mu}_1 &\geq \bm{0} & \text{dual feasibility} \\
\bm{\mu}_2 &\geq \bm{0} \\
\bm{\mu}_1^\top (\bm{A} \bm{x} - \bm{b}) &= \bm{0} & \text{complementary slackness} \\
-\bm{\mu}_2^\top \bm{x} &= \bm{0}
\end{aligned}
$$
