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
