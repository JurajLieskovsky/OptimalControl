# Controlability of LTI Discrete-Time Systems

The first $n+1$ states of a linear time-invariant system
$$
x_{k+1} = A x_k + B u_k, \quad x_k \in \Reals^n,\ u_k \in \Reals^m,
$$
assuming an initial state $x_0$ and a series of inputs $\{u_k\}_0^{N-1}$, can be expressed as
$$
\begin{aligned}
x_1 &= A x_0 + B u_0 \\
x_2 &= A^2 x_0 + A B u_0 + B u_1 \\
    &\vdots \\
x_n &= A^n x_0 + A^{n-1} B u_0 + A^{n-2} B u_1 + \ldots + B u_{n-1} \\
x_{n+1} &= A^{n+1} x_0 + A^{n} B u_0 + A^{n-1} B u_1 + A^{n-2} B u_2 + \ldots + B u_n
\end{aligned}
$$
For square matrices that satisfy their own characteristic equation the Cayley-Hamilton theorem states that for $N \geq n$ we may express $A^N$ as a linear combination of the lower matrix powers of $A$:
$$
A^N = a_0 I + a_1 A + \ldots + a_{n-1} A^{n-1}.
$$
Therefore, the state $x_{n+1}$ can be rewritten as
$$
x_{n+1} = A^{n+1} x_0 + A^{n-1} B (u_1 + a_{n-1} u_0) + A^{n-2} B (u_2 + a_{n-2} u_0) + \ldots + B (u_n + a_{0} u_0)
$$
which can be manipulated into the form
$$
x_{n+1} = A^{n+1} x_0 + R \begin{bmatrix}
	u_{n} + a_{0} u_0 \\
	u_{n-1} + a_{1} u_0 \\
	u_1 + a_{n-1} u_0
\end{bmatrix}.
$$
where
$$ 
R = \begin{bmatrix}
	B & AB & \dots & A^{n-1}B
\end{bmatrix}
$$
is the controllability matrix.

The same substitution can be applied also for subsequent timesteps up-to infinity, changing only the particular form of the vector of inputs' linear combinations. This has two consequences:
- All states reachable in $N > n$ steps are also reachable in $n$ steps (with unlimited inputs).
- If $R$ is rank deficient, some directions in the state-space cannot be effected by the inputs and therefore the system is uncontrollable.

