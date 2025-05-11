# Direct Linear-Quadratic MPC

The standard realization of an MPC controller is such that solves the optimization problem
$$
\begin{aligned}
	\min_{\{\bm{x}_k\}_{k=1}^{N}, \{\bm{u}_k\}_{k=0}^{N-1}} & \quad \bm{x}_N^\top \bm{Q}_N \bm{x}_N + \sum_{k=0}^{N-1} \bm{x}_k^\top \bm{Q} \bm{x}_k + \bm{u}_k^\top \bm{R} \bm{u}_k \\
	\text{s.t.} & \quad \bm{x}_{k+1} = \bm{A} \bm{x}_k + \bm{B} \bm{u}_k, \quad k = 0, \ldots, N-1 \\
							& \quad \bm{u}_{\min} \leq \bm{u}_k \leq \bm{u}_{\max}, \quad k = 0, \ldots, N-1
\end{aligned}
$$
where the initial state $\bm{x}_0$ is given[^1].

## Canonical QP form
### Optimized variables
$$
\begin{gathered}
	\bm{x} = \left[\begin{array}{cccc|cccc}
		\bm{u}_0^\top &
		\ldots &
		\ldots &
		\bm{u}_{N-1}^\top &
		\bm{x}_1^\top &
		\ldots &
		\ldots &
		\bm{x}_{N}^\top
	\end{array}\right]^\top
\end{gathered}
$$

### Objective function's terms
$$
\begin{gathered}
	\bm{P} = \left[\begin{array}{cccc|cccc}
		\bm{R} &        &        &        &        &        &        &        \\
		       & \ddots &        &        &        &        &        &        \\
		       &        & \ddots &        &        &        &        &        \\
		       &        &        & \bm{R} &        &        &        &        \\ \hline
		       &        &        &        & \bm{Q} &        &        &        \\
		       &        &        &        &        & \ddots &        &        \\
		       &        &        &        &        &        & \ddots &        \\
		       &        &        &        &        &        &        & \bm{Q}
	\end{array}\right]
	\,,\;
	\bm{q} = \left[\begin{array}{c}
		\bm{0} \\
		\vdots \\
		\vdots \\
		\bm{0} \\ \hline
		\bm{0} \\
		\vdots \\
		\vdots \\
		\bm{0}
	\end{array}\right]
\end{gathered}
$$

### Constraint's terms
$$
\begin{gathered}
	\bm{l} = \left[\begin{array}{c}
		- \bm{A} \bm{x}_0 \\
		\bm{0} \\
		\vdots \\
		\bm{0} \\ \hline
		\bm{u}_{\min} \\
		\vdots \\
		\vdots \\
		\bm{u}_{\min}
	\end{array}\right]
	\,,\;
	\bm{A} = \left[\begin{array}{cccc|cccc}
		\bm{B} &        &        &        &-\bm{I} &         &         &         \\
		       & \bm{B} &        &        &\bm{A}  & -\bm{I} &         &         \\
		       &        & \ddots &        &        & \ddots  & \ddots  &         \\ 
		       &        &        & \bm{B} &        &         & \bm{A}  & -\bm{I} \\ \hline
		\bm{I} &        &        &        &        &         &         &         \\
		       & \ddots &        &        &        &         &         &         \\
		       &        & \ddots &        &        &         &         &         \\
		       &        &        & \bm{I} &        &         &         &
	\end{array}\right]
	\,,\;
	\bm{u} = \left[\begin{array}{c}
		- \bm{A} \bm{x}_0 \\
		\bm{0} \\
		\vdots \\
		\bm{0} \\ \hline
		\bm{u}_{\max} \\
		\vdots \\
		\vdots \\
		\bm{u}_{\max}
	\end{array}\right]
\end{gathered}
$$

---

[^1]: If the dynamics $\bm{x}_{k+1} = \bm{A} \bm{x}_k + \bm{B} \bm{u}_k$ represent the linearized dynamics of a nonlinear system (i.e. $\bm{x}_k$ and $\bm{u}_k$ are in-fact $\bar{\bm{x}}_k = \bm{x}_k - \bm{x}^*$ and $\bar{\bm{u}}_k = \bm{u}_k - \bm{u}^*$) the value of $\bm{u}^*$ must be considered in the choice of limits $\bm{u}_{\min}$ and $\bm{u}_{\max}$.
