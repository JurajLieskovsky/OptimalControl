# Indirect Linear-Quadratic MPC

$$
\begin{aligned}
	\min_{\{\bm{u}_k\}_0^{N}} & \quad \bm{x}_k^\top \bm{Q} \bm{x}_k + \bm{u}_k^\top \bm{R} \bm{u}_k \\
	\text{s.t.} & \quad \bm{u}_{\min} \leq \bm{u}_k \leq \bm{u}_{\max} \,,
\end{aligned}
$$
where
$$
\bm{x}_{k} = \bm{A}^{k} \bm{x}_0 + \sum_{i=0}^{k-1} \bm{A}^{k-i-1}\bm{B}\bm{u}_{i} \,,\quad k = 0, \ldots, N+1
$$

