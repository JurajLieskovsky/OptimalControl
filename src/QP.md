# Quadratic Programming

Let us consider a constrained optimization problem in the form
$$
\begin{aligned}
	\min_{x} & \quad \frac{1}{2} x^\top Q x + c^\top x \\
	\text{s.t.} & \quad A x \leq b \,,
\end{aligned}
$$
where $Q \succeq 0$.

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

## Dual problem
The dual problem of the QP problem can be written as
$$
\begin{aligned}
\max_{\mu} & \enspace \underbrace{\min_{x} L(x,\mu)}_{q(\mu)}, \quad L(x,\mu) = \frac{1}{2} x^\top Q x + c^\top x + \mu^\top (Ax - b) \\
\text{s.t.} & \enspace \mu \geq 0 \\
            & \enspace \mu \in \{\mu \mid q(\mu) > -\infty\} ,
\end{aligned}
$$
where the Lagrangian can be manipulated into the form
$$
L(x,\mu) = \frac{1}{2} x^\top Q x + x^\top (c + A^\top \mu) - b^\top \mu .
$$
Its critical point can be found by solving
$$
\frac{\partial L}{\partial x}(x,\mu) = Qx + c + A^\top \mu = 0,
$$
which yields
$$
x = -Q^{-1} (c + A^\top \mu).
$$
When substituted back into the original dual problem, after basic manipulations, we attain
$$
\begin{aligned}
\max_{\mu} & \enspace q(\mu) = -\frac{1}{2}(c + A^\top \mu)^\top Q^{-1} (c + A^\top \mu) - b^\top \mu \\
\text{s.t.} & \enspace \mu \geq 0 \\
            & \enspace \mu \in \{\mu \mid q(\mu) > -\infty\} .
\end{aligned}
$$
