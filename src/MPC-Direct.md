# Direct formulation

$$
\begin{aligned}
	\min_{\{\bm{x}_k\}_1^{N+1}, \{\bm{u}_k\}_0^{N}} & \quad \bm{x}_k^\top \bm{Q} \bm{x}_k + \bm{u}_k^\top \bm{R} \bm{u}_k \\
	\text{s.t.} & \quad \bm{x}_{k+1} = \bm{A} \bm{x}_k + \bm{B} \bm{u}_k \\
							& \quad \bm{u}_{\min} \leq \bm{u}_k \leq \bm{u}_{\max} \,,
\end{aligned}
$$

## Canonical QP form
$$
\begin{gathered}
	\bm{x} = \left[\begin{array}{c}
		\bm{u}_0 \\
		\vdots \\
		\vdots \\
		\bm{u}_N \\ \hline
		\bm{x}_1 \\
		\vdots \\
		\vdots \\
		\bm{x}_{N+1}
	\end{array}\right]
	\,,\;
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
	\\
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
