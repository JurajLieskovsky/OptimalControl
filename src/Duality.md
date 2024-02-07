
# Lagrangian Duality

In the following section we will derive the so-called dual problem of a (primal) optimization problem, following the derivation demonstrated in a series of [short lectures](https://youtube.com/playlist?list=PL10NOnsbP5Q61XSVk-3yNOY2qLI-wTM6k&si=swJzRNlXSozeE2Rm) which accompany the book @@Bierlaire2018.
Possibly the most important property of the dual problem (from a practical point of view) is that it is convex even if the primal optimization problem is not @@Boyd2004.

Let us consider a constrained optimization problem in the form
$$
\begin{aligned}
	\min_{\bm{x}} & \quad \bm{f}(\bm{x}) \\
	\text{s.t.} & \quad \bm{g}(\bm{x}) ≤ \bm{0} \\
	            & \quad \bm{h}(\bm{x}) = \bm{0} \,,
\end{aligned}
$$
to which we will refer to as the primal problem. With regard to this problem, let us define the Lagrangian
$$
L(\bm{x},\bm{\lambda},\bm{\mu}) = \bm{f}(\bm{x}) + \bm{\lambda}^\top \bm{h}(\bm{x}) + \bm{\mu}^\top \bm{g}(\bm{x}) \,,
$$
where $\bm{\lambda}$ and $\bm{\mu}$ are Lagrange multipliers[^1].

Consequently, let us refer to a function that minimizes the Lagrangian for a given $\bm{\lambda}$ and $\bm{\mu}$ as the dual function:
$$
q(\bm{\lambda},\bm{\mu}) = \min_{\bm{x}} L(\bm{x},\bm{\lambda},\bm{\mu}) \,.
$$

### Theorem
Let $\bm{x}^*$ be the solution to the primal problem. If $\bm{\mu} \geq \bm{0}$, then
$$
q(\bm{\lambda},\bm{\mu}) \leq f(\bm{x}^*) \,.
$$

#### Proof 
$$
q(\bm{\lambda},\bm{\mu}) = \min_{\bm{x}} L(\bm{x},\bm{\lambda},\bm{\mu}) \leq L(\bm{x}^*,\bm{\lambda},\bm{\mu})
$$

(*For any $\bm{\lambda}$ and $\bm{\mu} \geq \bm{0}$, I can find $\bm{x}$ that minimizes the Lagrangian as well as or better than $\bm{x}^*$ by violating the constraints.*)

<!--. As an example, I can potentially find an $x$ that mismatches the signs of $\lambda_i$ and $h_i(x) \neq 0$ while not increasing the values of $f(x)$ and $g_i(x)$*)-->

and

$$
L(\bm{x}^*,\bm{\lambda},\bm{\mu}) = f(\bm{x}^*) + \bm{\lambda}^\top \underbrace{h(\bm{x}^*)}_{= \bm{0}} + \underbrace{\bm{\mu}^\top}_{\geq \bm{0}} \underbrace{g(\bm{x}^*)}_{\leq \bm{0}} \leq f(\bm{x}^*)
$$
(*Because if $\mu_i > 0$ and $g_i(\bm{x}^*) < 0$ then $\mu_i^\top g_i(\bm{x}^*) < 0$*)

$\Box$

#### Corollary
Let $\bm{x}^*$ be the solution to the primal problem and $\bm{x}$ feasible w.r.t its constraints. If $\bm{\lambda} \in \mathbb{R}^n$ and $\mu \in \mathbb{R}^p$, $\bm{\mu} \geq \bm{0}$, then
$$
q(\bm{\lambda},\bm{\mu}) \leq f(\bm{x}^*) \leq f(\bm{x}) \,.
$$

<!--(*This might be important for iterative approaches*)-->

## Dual problem
Consequently we may state the dual problem of finding the best lower bounds to the primal problem as
$$
\begin{aligned}
	\max_{\bm{\lambda},\bm{\mu}} & \enspace \underbrace{\min_{\bm{x}} L(\bm{x},\bm{\lambda},\bm{\mu})}_{q(\bm{\lambda},\bm{\mu})} \\
	\text{s.t.} & \enspace \bm{\mu} \geq \bm{0} \\
              & \enspace (\bm{\lambda}, \bm{\mu}) \in \{\bm{\lambda}, \bm{\mu} \mid q(\bm{\lambda}, \bm{\mu})>-\infty\} \,.
\end{aligned}
$$

(*The second condition means we are looking only for bounded solutions*)

### (Weak duality) theorem
If $\bm{x}^*$ is the solution to the primal problem and $(\bm{\lambda}^*,\bm{\mu}^*)$ is the solution to the dual problem, then 
$$
	q(\bm{\lambda}^*,\bm{\mu}^*) \leq f(\bm{x}^*) \,.
$$

#### Corollary

If one problem is unbounded the other is infeasible.

#### Corollary
If $\exists \ \bm{x}^*, \bm{\lambda}^*, \bm{\mu}^*$ such that
$$
	q(\bm{\lambda}^*,\bm{\mu}^*) = f(\bm{x}^*) \,,
$$
they are optimal.

---
[^1]: Note that $\bm{\mu} \geq \bm{0}$ must hold in order to penalize the violation of $\bm{g}(\bm{x}) \leq \bm{0}$. 
