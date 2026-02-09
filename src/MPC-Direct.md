# Trajectory Optimization Using OSQP

For embedded applications we may want to use QP solvers with code generation such as [OSQP](https://osqp.org/). The particular form of the QP program it solves lends itself to LQ trajectory optimization problems with additional box constraints, e.g.
$$
\begin{aligned}
  \tag{2a-c}
  \min_{x_{0:N}, u_{0:N-1}} & \quad q_N^\top \, x_N + \frac{1}{2} x_N^\top Q_N x_N + \sum_{k=0}^{N-1}
    \begin{bmatrix} q_k \\ r_k \end{bmatrix}^\top \begin{bmatrix} x_k \\ u_k \end{bmatrix} +
    \frac{1}{2} \begin{bmatrix} x_k \\ u_k \end{bmatrix}^\top \begin{bmatrix} Q_k & S_k^\top \\ S_k & R_k \end{bmatrix} \begin{bmatrix} x_k \\ u_k \end{bmatrix} \\
  \text{s.t.} & \quad x_{k+1} = A_k x_k + B_k u_k + c_k, \quad k = 0, \ldots, N-1 \\
              & \quad x_0 = \hat{x}_0 \\
							& \quad x_{\min} \leq x_k \leq x_{\max}, \quad \forall k \in [0, N] \\
							& \quad u_{\min} \leq u_k \leq u_{\max}, \quad \forall k \in [0, N-1]
\end{aligned}
$$

## OSQP form
To coincide with the form of the QP program described in the [documentation of OSQP](https://osqp.org/docs/) we define a vector of decision variables
$$
\begin{gathered}
	x = \left[\begin{array}{ccc|cccc}
		u_0^\top &
		\ldots &
		u_{N-1}^\top &
		x_0^\top &
		\ldots &
		x_{N-1}^\top & 
		x_{N}^\top
	\end{array}\right]^\top
\end{gathered}
$$
for which the objective function contains the terms
$$
\begin{gathered}
	P = \left[\begin{array}{ccc|cccc}
		R_1      &        &               & S_k &        &          &       \\
		         & \ddots &               &     & \ddots &          &       \\
		         &        & R_{N-1}       &     &        & S_{N-1}  &       \\ \hline
		S_1^\top &        &               & Q_k &        &          &       \\
		         & \ddots &               &     & \ddots &          &       \\
		         &        & S_{N-1}^\top  &     &        & Q_{N-1}  &       \\
					   &        &               &     &        &          & Q_{N}
	\end{array}\right]
	\,,\;
	q = \left[\begin{array}{c}
		r_0 \\
		\vdots \\
		r_{N-1} \\ \hline
		q_0 \\
		\vdots \\
		q_{N-1} \\
		q_N
	\end{array}\right].
\end{gathered}
$$
The constrains are then incorporated using
$$
\begin{gathered}
	l = \left[\begin{array}{c}
		-\hat{x}_0 \\
		-c_0 \\
		\vdots \\
		-c_{N-1} \\ \hline
		x_{\min} \\
		\vdots \\
		\vdots \\
		x_{\min} \\ \hline
		u_{\min} \\
		\vdots \\
		u_{\min}
	\end{array}\right]
	\,,\;
	A = \left[\begin{array}{ccc|cccc}
		 0   &        &         & -I  &        &         &    \\
		 B_0 &        &         & A_0 & -I     &         &    \\
		     & \ddots &         &     & \ddots & \ddots  &    \\ 
		     &        & B_{N-1} &     &        & A_{N-1} & -I \\ \hline
         &        &         & I   &        &         &    \\  
         &        &         &     & \ddots &         &    \\  
         &        &         &     &        & \ddots  &    \\  
         &        &         &     &        &         & I  \\ \hline      
		 I   &        &         &     &        &         &    \\
		     & \ddots &         &     &        &         &    \\
		     &        & I       &     &        &         &
	\end{array}\right]
	\,,\;
	u = \left[\begin{array}{c}
		-\hat{x}_0 \\
		-c_0 \\
		\vdots \\
		-c_{N-1} \\ \hline
		x_{\max} \\
		\vdots \\
		\vdots \\
		x_{\max} \\ \hline
		u_{\max} \\
		\vdots \\
		u_{\max}
	\end{array}\right].
\end{gathered}
$$
