The vast majority of numerical optimization problems can be written in the form
$$
\begin{aligned}
	\min_{x} & \quad f(x) \\
	\text{s.t.} & \quad g(x) ≤ 0 \\
	            & \quad h(x) = 0,
\end{aligned}
$$
where $x \in \mathbb{R}^n$ are optimized variables, $f : \mathbb{R}^n \rightarrow \mathbb{R}$ is the objective function, $g : \mathbb{R}^n \rightarrow \mathbb{R}^r$ are inequality constraints and $h : \mathbb{R}^n \rightarrow \mathbb{R}^s$ are equality constraints. Here we assume that $n$, $r$, and $s$ lie in $\mathbb{N}$ and that constraints $g$ and $h$ define a non-empty set of feasible solutions.

Based on the properties of $f$, $g$, and $h$, different approaches can be taken to solve the optimization problem. For example, if the objective function is convex and the constraint are affine the problem has a unique solution (optimal value of the objective function) that can be found using gradient descend. In this course we will focus on this type of problems which are classified as *convex*.

We will start with a general overview of [Lagrangian Duality](Duality.md) and [KKT conditions](KKT.md) which are applicable to both convex and non-convex optimization problems. Then we will describe two specific types of convex optimization problems: linear programming (LP) and quadratic programming (QP). 
