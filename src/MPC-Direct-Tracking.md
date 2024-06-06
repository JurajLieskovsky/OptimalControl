# Reference Tracking with Direct LQ MPC
If we aim to track a reference $\{\bm{w}_k\}_{k=1}^N$ with the system's output
$$
\bm{y}_k = \bm{C} \bm{x}_k,
$$
we may define and error $\bm{e}_k = \bm{y}_k - \bm{w}_k$ and formulate an MPC problem
$$
\begin{aligned}
	\min_{\{\bm{x}_k\}_{k=1}^{N+1}, \{\bm{u}_k\}_{k=0}^{N}} & \quad \|\bm{e}_k||_{\bm{Q}}^2 + \|\bm{u}_k||_{\bm{R}}^2 \\
	\text{s.t.} & \quad \bm{x}_{k+1} = \bm{A} \bm{x}_k + \bm{B} \bm{u}_k \\
							& \quad \bm{u}_{\min} \leq \bm{u}_k \leq \bm{u}_{\max},
\end{aligned}
$$
where the running cost is equivalent to
$$
(\bm{C} \bm{x}_k - \bm{w}_k)^\top \bm{Q} (\bm{C} \bm{x}_k - \bm{w}_k) + \bm{u}_k^\top \bm{R} \bm{u}_k,
$$
which further expands to
$$
\bm{x}_k^\top \bm{C}^\top \bm{Q} \, \bm{C} \, \bm{x}_k - 2 \bm{w}_k^\top \bm{Q} \, \bm{C} \, \bm{x}_k + \underbrace{\bm{w}_k^\top \bm{Q} \, \bm{w}_k}_{\mathrm{const.}} + \bm{u}_k^\top \bm{R} \, \bm{u}_k.
$$

## Canonical QP form
### Optimized variables
$$
\begin{gathered}
	\bm{x} = \left[\begin{array}{cccc|cccc}
		\bm{u}_0^\top &
		\ldots &
		\ldots &
		\bm{u}_N^\top &
		\bm{x}_1^\top &
		\ldots &
		\ldots &
		\bm{x}_{N+1}^\top
	\end{array}\right]^\top
\end{gathered}
$$

### Objective function's terms
$$
\begin{gathered}
  \def\arraystretch{1.3}
  \bm{P} = \left[\begin{array}{cccc|cccc}
		\bm{R} &        &        &        &                              &        &        &        \\
		       & \ddots &        &        &                              &        &        &        \\
		       &        & \ddots &        &                              &        &        &        \\
		       &        &        & \bm{R} &                              &        &        &        \\ \hline
		       &        &        &        & \bm{C}^\top \bm{Q} \, \bm{C} &        &        &        \\
		       &        &        &        &                              & \ddots &        &        \\
		       &        &        &        &                              &        & \ddots &        \\
		       &        &        &        &                              &        &        & \bm{C}^\top \bm{Q} \, \bm{C}
	\end{array}\right]
	\,,\;
	\bm{q} = \left[\begin{array}{c}
		\bm{0} \\
		\vdots \\
		\vdots \\
		\bm{0} \\ \hline
		- \bm{C}^\top \bm{Q} \, \bm{w}_k \\ 
		\vdots \\
		\vdots \\
		- \bm{C}^\top \bm{Q} \, \bm{w}_k 
	\end{array}\right]
\end{gathered}
$$

#### Constraint's terms
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
