# Controllability/Reachability of an LTI system

Controllability and reachability are defined for discrete-time systems as:

- A system is controllable if from any state $x_0 \in \Reals^n$ one can achieve the state $x_N = 0$ using a series of inputs $\{u_k\}_0^{N-1}$.
- A state $x_N \in \Reals^n$ is reachable if it can be achieved by applying a series of inputs $\{u_k\}_0^{N-1}$ when starting from the initial state $x_0 = 0$.

For continuous-time systems they are similarly defined as:

- A system is controllable if from any state $x(0) \in \Reals^n$ one can achieve the state $x(t) = 0$ using a control policy $u(\tau)$, $\tau \in \langle 0, t)$.
- A state $x(t) \in \Reals^n$ is reachable if it can be achieved by applying a control policy $u(\tau)$, $\tau \in \langle 0, t)$ when starting from the initial state $x(0) = 0$.

For linear systems all states are reachable if the system is controllable.

## Discrete time

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

## Continuous time

The state of a linear time-invariant system
$$
\dot{x}(\tau) = Ax(\tau) + Bu(\tau), \quad x(\tau) \in \Reals^n,\ u(\tau) \in \Reals^m
$$ at time $t$, starting from the initial state $x(0)$ and influenced by a continuous input $u(\tau)$, can be expressed as
$$
x(t) = e^{At} x(0) + \int_0^t e^{A(t-τ)} B u(τ)\ dτ. \tag{1}
$$
For square matrices that satisfy their own characteristic equation the Cayley-Hamilton theorem has a consequence that the inifinite series
$$
e^{At} = I + At + \frac{(At)^2}{2!} + \ldots
$$
can be expressed using a finite number of terms
$$
e^{At} = ϕ_0(t) I + ϕ_1(t) A + \dots + ϕ_{n-1}(t) A^{n-1}.
$$
After substituting it back into the second term of (1) we attain
$$
x(t) = e^{At} x(0) + \int_0^t \big( ϕ_0(t-τ)\, I + ϕ_1(t-τ)\, A + \dots + ϕ_{n-1}(t-τ)\, A^{n-1} \big) B u(\tau) \, dτ
$$
which can be further manipulated into the form
$$
x(t) = e^{At} x(0) + R
\int_0^t
\begin{bmatrix}
	ϕ_0(t-τ)\ u(τ)\\
	ϕ_1(t-τ)\ u(τ)\\
	\vdots \\
	ϕ_{n-1}(t-τ)\ u(τ)\\
\end{bmatrix}
dτ,
$$
where
$$ 
R = \begin{bmatrix}
	B & AB & \dots & A^{n-1}B
\end{bmatrix}
$$
is the controllability matrix. If $R$ is rank deficient, some directions in the state-space cannot be effected by the inputs and therefore the system is uncontrollable.
