
# Lagrangian Duality

In the following section we will derive the so-called dual problem of a (primal) optimization problem, following the derivation demonstrated in a series of [short lectures](https://youtube.com/playlist?list=PL10NOnsbP5Q61XSVk-3yNOY2qLI-wTM6k&si=swJzRNlXSozeE2Rm) which accompany the book @@Bierlaire2018.
Possibly the most important property of the dual problem (from a practical point of view) is that it is convex even if the primal optimization problem is not @@Boyd2004.

Let us consider a constrained optimization problem in the form
$$
\begin{aligned}
	\min_{x} & \quad f(x) \\
	\text{s.t.} & \quad g(x) ≤ 0 \\
	            & \quad h(x) = 0,
\end{aligned}
$$
to which we will refer to as the primal problem. With regard to this problem, let us define the Lagrangian
$$
L(x,\lambda,\mu) = f(x) + \lambda^\top h(x) + \mu^\top g(x),
$$
where $\lambda$ and $\mu$ are Lagrange multipliers, and the dual function
$$
q(\lambda,\mu) = \min_{x} L(x,\lambda,\mu).
$$

### Theorem
Let $x^*$ be the solution to the primal problem. If $\mu \geq 0$, then
$$
q(\lambda,\mu) \leq f(x^*).
$$

#### Proof 
$$
q(\lambda,\mu) = \min_{x} L(x,\lambda,\mu) \leq L(x^*,\lambda,\mu)
$$

(*For any $\lambda$ and $\mu \geq 0$, I can find $x$ that minimizes the Lagrangian as well as or better than $x^*$ by violating the constraints.*)

<!--. As an example, I can potentially find an $x$ that mismatches the signs of $\lambda_i$ and $h_i(x) \neq 0$ while not increasing the values of $f(x)$ and $g_i(x)$*)-->

and

$$
L(x^*,\lambda,\mu) = f(x^*) + \lambda^\top \underbrace{h(x^*)}_{= 0} + \underbrace{\mu^\top}_{\geq 0} \underbrace{g(x^*)}_{\leq 0} \leq f(x^*)
$$
(*Because if $\mu_i > 0$ and $g_i(x^*) < 0$ then $\mu_i^\top g_i(x^*) < 0$*)

$\Box$

#### Corollary
Let $x^*$ be the solution to the primal problem and $x$ feasible w.r.t its constraints. If $\lambda \in \mathbb{R}^n$ and $\mu \in \mathbb{R}^p$, $\mu \geq 0$, then
$$
q(\lambda,\mu) \leq f(x^*) \leq f(x).
$$

<!--(*This might be important for iterative approaches*)-->

## Dual problem
Consequently we may state the dual problem of finding the best lower bounds to the primal problem as
$$
\begin{aligned}
	\max_{\lambda,\mu} & \enspace \underbrace{\min_{x} L(x,\lambda,\mu)}_{q(\lambda,\mu)} \\
	\text{s.t.} & \enspace \mu \geq 0 \\
              & \enspace (\lambda, \mu) \in \{\lambda, \mu \mid q(\lambda, \mu)>-\infty\}.
\end{aligned}
$$

(*The second condition means we are looking only for bounded solutions*)

### (Weak duality) theorem
If $x^*$ is the solution to the primal problem and $(\lambda^*,\mu^*)$ is the solution to the dual problem, then 
$$
	q(\lambda^*,\mu^*) \leq f(x^*).
$$

#### Corollary

If one problem is unbounded the other is infeasible.

#### Corollary
If $\exists \ x^*, \lambda^*, \mu^*$ such that
$$
	q(\lambda^*,\mu^*) = f(x^*),
$$
they are optimal.

---
[^1]: Note that $\mu \geq 0$ must hold in order to penalize the violation of $g(x) \leq 0$. 
