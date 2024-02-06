# Karuch-Kuhn-Tucker (KKT) Conditions

The Karuch-Kuhn-Tucker (KKT) conditions are first order necessary conditions for finding the solution of an optimization problem in the form
$$
\begin{aligned}
	\text{minimize:}& \quad f(\bm{x}) \\
	\text{subject to:}& \quad \bm{g}(\bm{x}) ≤ \bm{0} \\
	                  & \quad \bm{h}(\bm{x}) = \bm{0} \,.
\end{aligned}
$$
Furthermore, they are also sufficient conditions for convex problems, i.e. those where $\bm{f}(\bm{x})$, $\bm{g}(\bm{x})$ are convex and $\bm{h}(\bm{x})$ is affine (linear) @@Boyd2004.

The conditions are as follows: 
- stationarity
$$
	∇f(\bm{x}) + \bm{\mu}^T ∇\bm{g}(\bm{x}) + \bm{\lambda}^T ∇\bm{h}(\bm{x}) = \bm{0}
$$
(*The linear combination of the constraints' gradients has to be equal the objective function's gradient. In the case of a single equality constraint, this means that the constraint needs to be collinear with the contour of the objective function*)

- primal feasibility
$$
\begin{aligned}
	\bm{g}(\bm{x}) ≤ \bm{0} \\
	\bm{h}(\bm{x}) = \bm{0} \\
\end{aligned}
$$
(*Constraints of the stated optimization problem have to be satisfied*)

- dual feasibility
$$
\bm{\mu} \geq \bm{0} \\
$$
(*For $\bm{g}(\bm{x}) > \bm{0}$ the inequality $\mu^\top \bm{g}(\bm{x}) \geq \bm{0}$ must hold*)

- complementary slackness
$$
\bm{\mu}^\top \bm{g}(\bm{x}) = 0 \\
$$
(*If $\bm{x}$ lies inside the feasible set w.r.t to the condition $\bm{g}(\bm{x}) \leq 0$, then $\bm{\mu} = \bm{0}$. If it instead lies on the boundary, then $\bm{\mu} \geq \bm{0}$*)
