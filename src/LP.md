# Linear Programming

Let us consider a constrained optimization problem in the form
$$
\begin{aligned}
	\max_{x} & \quad c^\top x \\
	\text{s.t.} & \quad A x \leq b \\
	            & \quad x \geq 0 \,.
\end{aligned}
$$

As both the objective function and constraints are linear the problem is convex. For this reason KKT conditions are not only necessary but also sufficient if a feasible $x$ w.r.t the constraints exists.

## KKT conditions
The KKT conditions of this problem can be states as:
$$
\begin{aligned}
c + A^\top \mu_1 - \mu_2 &= 0 & \text{stationarity} \\
A x &\leq b & \text{primal feasibility} \\
x &\geq 0 & \\ 
\mu_1 &\geq 0 & \text{dual feasibility} \\
\mu_2 &\geq 0 \\
\mu_1^\top (A x - b) &= 0 & \text{complementary slackness} \\
-\mu_2^\top x &= 0
\end{aligned}
$$

## Dual problem
The dual problem of the LP problem can be written as
$$
\begin{aligned}
\max_{\mu_1, \mu_2} & \enspace \underbrace{\min_{x} L(x,\mu_1, \mu_2)}_{q(\mu_1, \mu_2)}, \quad L(x,\mu_1,\mu_2) = -c^\top x - \mu_1^\top x + \mu_2^\top (Ax - b) \\
\text{s.t.} & \enspace \mu_1 \geq 0 \\
            & \enspace \mu_2 \geq 0 \\
            & \enspace (\mu_1,\mu_2) \in \{\mu_1, \mu_2 \mid q(\mu_1, \mu_2) > -\infty\} ,
\end{aligned}
$$
where the Lagrangian can be manipulated into the form
$$
L(x,\mu_1,\mu_2) = x^\top (A^\top \mu_2 - \mu_1 - c) - b^\top \mu_2.
$$
As we are only looking for bound solutions (last constraint) the condition
$$
A^\top \mu_2 - \mu_1 - c = 0
$$
must be satisfied and therefore
$$
\mu_1 = A^\top \mu_2 - c
$$
When substituted back into the original dual problem, after basic manipulations, we attain
$$
\begin{aligned}
\min_{\mu_2} & \enspace b^\top \mu_2 \\
\text{s.t.} & \enspace A^\top \mu_2 \geq c \\
            & \enspace \mu_2 \geq 0 \\
\end{aligned}
$$
