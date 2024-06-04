# Karuch-Kuhn-Tucker (KKT) Conditions

The Karuch-Kuhn-Tucker (KKT) conditions are first order necessary conditions for finding the solution of an optimization problem in the form
$$
\begin{aligned}
	\min_x& \quad f(\bm{x}) \\
	\text{s.t.}& \quad \bm{g}(\bm{x}) ≤ \bm{0} \\
	                  & \quad \bm{h}(\bm{x}) = \bm{0} \,.
\end{aligned}
$$
Furthermore, they are also sufficient conditions for convex problems, i.e. those where $\bm{f}(\bm{x})$, $\bm{g}(\bm{x})$ are convex and $\bm{h}(\bm{x})$ is affine (linear) @@Boyd2004.

The conditions are as follows: 
- stationarity
$$
	∇f(\bm{x}) + \bm{\mu}^\top ∇\bm{g}(\bm{x}) + \bm{\lambda}^\top ∇\bm{h}(\bm{x}) = \bm{0}
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
(*For a given $\bm{x}$, the columns of $∇\bm{g}(\bm{x})$ define a polyhedral cone in which $\bm{\mu}^\top ∇\bm{g}(\bm{x})$ must lie*.)

- complementary slackness
$$
\bm{\mu}^\top \bm{g}(\bm{x}) = 0 \\
$$
(*If $\bm{x}$ lies inside the feasible set w.r.t to the condition $\bm{g}(\bm{x}) \leq \bm{0}$, then $\bm{\mu} = \bm{0}$ and therefore $\bm{\mu}^\top ∇\bm{g}(\bm{x}) = \bm{0}$.*)
