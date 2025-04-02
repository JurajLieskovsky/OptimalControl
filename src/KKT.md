# Karuch-Kuhn-Tucker Conditions

The Karuch-Kuhn-Tucker (KKT) conditions are first order necessary conditions for finding the solution of an optimization problem in the form
$$
\begin{aligned}
	\min_x& \quad f(x) \\
	\text{s.t.}& \quad g(x) ≤ 0 \\
	                  & \quad h(x) = 0 \,.
\end{aligned}
$$
Furthermore, they are also sufficient conditions for convex problems, i.e. those where $f(x)$, $g(x)$ are convex and $h(x)$ is affine (linear) @@Boyd2004.

A solution satisfying these conditions gives us not only $x$ but also the Lagrange multipliers $\lambda$ and $\mu$ present in the Lagrangian
$$
L(x,\lambda,\mu) = f(x) + \lambda^\top h(x) + \mu^\top g(x).
$$

The conditions are as follows: 
- stationarity
$$
	∇f(x) + ∇g(x) \, \mu + ∇h(x) \, \lambda = 0 \tag{1}
$$
(*The linear combination of the constraints' gradients has to be equal to the objective function's gradient.*)

- primal feasibility
$$
\begin{align}
	g(x) &\leq 0 \\
	h(x) &= 0
\end{align} \tag{2-3}
$$
(*Constraints of the stated optimization problem have to be satisfied.*)

- dual feasibility
$$
\mu \geq 0 \tag{4}
$$
(*For a given $x$, the columns of $∇g(x)$ define a polyhedral cone in which $\mu^\top ∇g(x)$ must lie*.)

- complementary slackness
$$
\mu^\top g(x) = 0 \tag{5}
$$
(*If $x$ lies inside the feasible set w.r.t to the condition $g(x) < 0$, then $\mu = 0$ and therefore $\mu^\top ∇g(x) = 0$.*)

## Physical interpretation

The KKT conditions can be intuitively derived though an analogy where $\nabla f(x)$ is a potential field, for example of gravity of magnetism. Let us first address only the inequality constrained case
$$
\begin{aligned}
	\min_x& \quad f(x) \\
	\text{s.t.}& \quad g(x) ≤ 0,
\end{aligned}
$$
where the inequality constraints can be regarded as physical barriers. If we then recall the Lagrangian
$$
L(x,\lambda,\mu) = f(x) + \mu^\top g(x),
$$
the multipliers and $\mu$ can be viewed as contact forces acting against the influence of the potential field.

From this analogy we can immediately recover the dual feasibility and complementary slackness conditions (4-5) as contact forces can only be positive and do not act at a distance. The stationarity condition (1) (without the term related to the equality constraint) can then be interpreted as the contact forces and the pull of potential field being in equilibrium, which must occur at a local minima. Lastly, we are considering only solutions within the bounds of the inequality constraints, as if we were initially placed within them, satisfying the primal feasibility condition (2).

To incorporate equality constraints into this analogy we can simply reformulate them as
$$
0 \leq h(x) \leq 0
$$
likening them to being sandwiched between two surfaces. As we are always in contact there is no need for a complementary slackness condition and due to its bi-directional nature, elements of $\lambda$ can be both positive and negative. Therefore we must only include a primal feasibilty condition (2) and add an additional term to the stationarity condition (1).
