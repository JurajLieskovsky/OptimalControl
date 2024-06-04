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

## Dual problem
The dual problem of the LP problem can be written as
$$
\begin{aligned}
\max_{\bm{\mu}_1, \bm{\mu}_2} & \enspace \underbrace{\min_{\bm{x}} L(\bm{x},\bm{\mu}_1, \bm{\mu}_2)}_{q(\bm{\mu}_1, \bm{\mu}_2)}, \quad L(\bm{x},\bm{\mu}_1,\bm{\mu}_2) = -\bm{c}^\top \bm{x} - \bm{\mu}_1^\top \bm{x} + \bm{\mu}_2^\top (\bm{A}\bm{x} - \bm{b}) \\
\text{s.t.} & \enspace \bm{\mu}_1 \geq \bm{0} \\
            & \enspace \bm{\mu}_2 \geq \bm{0} \\
            & \enspace (\bm{\mu}_1,\bm{\mu}_2) \in \{\bm{\mu}_1, \bm{\mu}_2 \mid q(\bm{\mu}_1, \bm{\mu}_2) > -\infty\} ,
\end{aligned}
$$
where the Lagrangian can be manipulated into the form
$$
L(\bm{x},\bm{\mu}_1,\bm{\mu}_2) = \bm{x}^\top (\bm{A}^\top \bm{\mu}_2 - \bm{\mu}_1 - \bm{c}) - \bm{b}^\top \bm{\mu}_2.
$$
As we are only looking for bound solutions (last constraint) the condition
$$
\bm{A}^\top \bm{\mu}_2 - \bm{\mu}_1 - \bm{c} = 0
$$
must be satisfied and therefore
$$
\bm{\mu}_1 = \bm{A}^\top \bm{\mu}_2 - \bm{c}
$$
When substituted back into the original dual problem, after basic manipulations, we attain
$$
\begin{aligned}
\min_{\bm{\mu}_2} & \enspace \bm{b}^\top \bm{\mu}_2 \\
\text{s.t.} & \enspace \bm{A}^\top \bm{\mu}_2 \geq \bm{c} \\
            & \enspace \bm{\mu}_2 \geq \bm{0} \\
\end{aligned}
$$
