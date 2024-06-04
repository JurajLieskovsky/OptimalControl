# Quadratic Programming

Let us consider a constrained optimization problem in the form
$$
\begin{aligned}
	\min_{\bm{x}} & \quad \frac{1}{2} \bm{x}^\top \bm{Q} \bm{x} + \bm{c}^\top \bm{x} \\
	\text{s.t.} & \quad \bm{A} \bm{x} \leq \bm{b} \,,
\end{aligned}
$$
where $\bm{Q} \succeq 0$.

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

## Dual problem
The dual problem of the QP problem can be written as
$$
\begin{aligned}
\max_{\bm{\mu}} & \enspace \underbrace{\min_{\bm{x}} L(\bm{x},\bm{\mu})}_{q(\bm{\mu})}, \quad L(\bm{x},\bm{\mu}) = \frac{1}{2} \bm{x}^\top \bm{Q} \bm{x} + \bm{c}^\top \bm{x} + \bm{\mu}^\top (\bm{A}\bm{x} - \bm{b}) \\
\text{s.t.} & \enspace \bm{\mu} \geq \bm{0} \\
            & \enspace \bm{\mu} \in \{\bm{\mu} \mid q(\bm{\mu}) > -\infty\} ,
\end{aligned}
$$
where the Lagrangian can be manipulated into the form
$$
L(\bm{x},\bm{\mu}) = \frac{1}{2} \bm{x}^\top \bm{Q} \bm{x} + \bm{x}^\top (\bm{c} + \bm{A}^\top \bm{\mu}) - \bm{b}^\top \bm{\mu} .
$$
Its critical point can be found by solving
$$
\frac{\partial L}{\partial \bm{x}}(\bm{x},\bm{\mu}) = \bm{Q}\bm{x} + \bm{c} + \bm{A}^\top \bm{\mu} = \bm{0},
$$
which yields
$$
\bm{x} = -\bm{Q}^{-1} (\bm{c} + \bm{A}^\top \bm{\mu}).
$$
When substituted back into the original dual problem, after basic manipulations, we attain
$$
\begin{aligned}
\max_{\bm{\mu}} & \enspace q(\bm{\mu}) = -\frac{1}{2}(\bm{c} + \bm{A}^\top \bm{\mu})^\top \bm{Q}^{-1} (\bm{c} + \bm{A}^\top \bm{\mu}) - \bm{b}^\top \bm{\mu} \\
\text{s.t.} & \enspace \bm{\mu} \geq \bm{0} \\
            & \enspace \bm{\mu} \in \{\bm{\mu} \mid q(\bm{\mu}) > -\infty\} .
\end{aligned}
$$
