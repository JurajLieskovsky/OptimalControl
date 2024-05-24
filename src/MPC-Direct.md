# Direct linear-quadratic MPC

## Standard formulation

The most typical realization of an MPC controller is such that solves the optimization problem
$$
\begin{aligned}
	\min_{\{\bar{\bm{x}}_k\}_1^{N+1}, \{\bar{\bm{u}}_k\}_0^{N}} & \quad \bar{\bm{x}}_k^\top \bm{Q} \bar{\bm{x}}_k + \bar{\bm{u}}_k^\top \bm{R} \bar{\bm{u}}_k \\
	\text{s.t.} & \quad \bar{\bm{x}}_{k+1} = \bm{A} \bar{\bm{x}}_k + \bm{B} \bar{\bm{u}}_k \\
							& \quad \bm{u}_{\min} - \bm{u}^* \leq \bar{\bm{u}}_k \leq \bm{u}_{\max} - \bm{u}^* \,.
\end{aligned}
$$
It is particular useful for regulating systems around a fixed point $\{\bm{x}^*,\bm{u}^*\}$ where $\bm{u}^* = \bm{0}$. The downside of this formulation is that if $\bm{u}^* \neq \bm{0}$ we are in-fact not minimizing the inputs as a whole but only their deviations from the fixed point.

### Canonical QP form
#### Optimized variables
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

#### Objective function's terms
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

## Alternative formulation
Assuming we have linearized the system in a fixed point we may describe the MPC problem as
$$
\begin{aligned}
	\min_{\{\bm{x}_k\}_1^{N+1}, \{\bm{u}_k\}_0^{N}} & \quad (\bm{x}_k - \bm{x}_{k_\mathrm{ref}})^\top \bm{Q} (\bm{x}_k - \bm{x}_{k_\mathrm{ref}}) + \bm{u}_k^\top \bm{R} \bm{u}_k \\
	\text{s.t.} & \quad \bm{x}_{k+1} - \bm{x}^* = \bm{A} (\bm{x}_k - \bm{x}^*) + \bm{B} (\bm{u}_k - \bm{u}^*) \\
							& \quad \bm{u}_{\min} \leq \bm{u}_k \leq \bm{u}_{\max} \,,
\end{aligned}
$$

where the running cost expands to
$$
\bm{x}_k^\top \bm{Q} \bm{x}_k - 2 \bm{x}_{k_\mathrm{ref}}^\top \bm{Q} \bm{x}_k + \underbrace{\bm{x}_{k_\mathrm{ref}}^\top \bm{Q} \bm{x}_{k_\mathrm{ref}}}_{\mathrm{const.}} + \bm{u}_k^\top \bm{R} \bm{u}_k
$$
and dynamics' constraint can be manipulated so that optimized variables are separated from constant terms
$$
\underbrace{\bm{A} \bm{x}^* + \bm{B} \bm{u}^* - \bm{x}^*}_{\bm{b}^*} = \bm{A} \bm{x}_k + \bm{B} \bm{u}_k - \bm{x}_{k+1} \,.
$$
There are two major differences between this and the standard formulation.
1. Inputs $\bm{u}_k$ figure directly the term $\bm{u}_k^\top \bm{R} \bm{u}_k$ of the objective function,
2. deviations of states are evaluated in relation to $\bm{x}_{k_\mathrm{ref}}$ which is useful for tracking problems as their values can differ on the optimization's horizon.

### Canonical QP form
#### Optimized variables
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
#### Objective function's terms
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
		-\bm{Q} \bm{x}_{k_{\mathrm{ref}}} \\
		\vdots \\
		\vdots \\
		-\bm{Q} \bm{x}_{k_{\mathrm{ref}}}
	\end{array}\right]
\end{gathered}
$$
#### Constraints' terms
$$
\begin{gathered}
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
	\\
	\bm{l} = \left[\begin{array}{c}
		\bm{b}^*- \bm{A} \bm{x}_0 \\
		\bm{b}^* \\
		\vdots \\
		\bm{b}^* \\ \hline
		\bm{u}_{\min} \\
		\vdots \\
		\vdots \\
		\bm{u}_{\min}
	\end{array}\right]
	\,,\;
	\bm{u} = \left[\begin{array}{c}
		\bm{b}^* - \bm{A} \bm{x}_0 \\
		\bm{b}^* \\
		\vdots \\
		\bm{b}^* \\ \hline
		\bm{u}_{\max} \\
		\vdots \\
		\vdots \\
		\bm{u}_{\max}
	\end{array}\right]
\end{gathered}
$$
