# Trajectory Optimization Using MPC

$$
\begin{aligned}
	\min_{\{x_k\}_{k=1}^{N}, \{u_k\}_{k=0}^{N-1}} & \quad x_N^\top Q_N x_N + \sum_{k=0}^{N-1} x_k^\top Q x_k + u_k^\top R u_k \\
	\text{s.t.} & \quad x_{k+1} = A x_k + B u_k, \quad k = 0, \ldots, N-1 \\
							& \quad u_{\min} \leq u_k \leq u_{\max}, \quad k = 0, \ldots, N-1
\end{aligned}
$$

## Canonical QP form
### Optimized variables
$$
\begin{gathered}
	x = \left[\begin{array}{cccc|cccc}
		u_0^\top &
		\ldots &
		\ldots &
		u_{N-1}^\top &
		x_1^\top &
		\ldots &
		\ldots &
		x_{N}^\top
	\end{array}\right]^\top
\end{gathered}
$$

### Objective function's terms
$$
\begin{gathered}
	P = \left[\begin{array}{cccc|cccc}
		R &        &        &        &        &        &        &        \\
		       & \ddots &        &        &        &        &        &        \\
		       &        & \ddots &        &        &        &        &        \\
		       &        &        & R &        &        &        &        \\ \hline
		       &        &        &        & Q &        &        &        \\
		       &        &        &        &        & \ddots &        &        \\
		       &        &        &        &        &        & \ddots &        \\
		       &        &        &        &        &        &        & Q
	\end{array}\right]
	\,,\;
	q = \left[\begin{array}{c}
		0 \\
		\vdots \\
		\vdots \\
		0 \\ \hline
		0 \\
		\vdots \\
		\vdots \\
		0
	\end{array}\right]
\end{gathered}
$$

### Constraint's terms
$$
\begin{gathered}
	l = \left[\begin{array}{c}
		- A x_0 \\
		0 \\
		\vdots \\
		0 \\ \hline
		u_{\min} \\
		\vdots \\
		\vdots \\
		u_{\min}
	\end{array}\right]
	\,,\;
	A = \left[\begin{array}{cccc|cccc}
		B &        &        &        &-I &         &         &         \\
		       & B &        &        &A  & -I &         &         \\
		       &        & \ddots &        &        & \ddots  & \ddots  &         \\ 
		       &        &        & B &        &         & A  & -I \\ \hline
		I &        &        &        &        &         &         &         \\
		       & \ddots &        &        &        &         &         &         \\
		       &        & \ddots &        &        &         &         &         \\
		       &        &        & I &        &         &         &
	\end{array}\right]
	\,,\;
	u = \left[\begin{array}{c}
		- A x_0 \\
		0 \\
		\vdots \\
		0 \\ \hline
		u_{\max} \\
		\vdots \\
		\vdots \\
		u_{\max}
	\end{array}\right]
\end{gathered}
$$

---
