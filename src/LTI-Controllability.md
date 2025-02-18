# Controllability/Reachability of an LTI system

## Discrete-time

The state of a linear time-invariant system
$$
x_{k+1} = A x_k + B u_k, \quad x_k \in \Reals^n,\ u_k \in \Reals^m
$$
at step $N$, assuming an initial state $\bm{x}_0$ and a series of inputs $\{\bm{u}_k\}_0^{N-1}$, can be expressed as
$$
x_N = A^N x_0 + A^{N-1} B u_0 + A^{N-2} B u_1 + \ldots + B u_{N-1}
$$
For square matrices that satisfy their own characteristic equation the Cayley-Hamilton theorem states that for $N \geq n$ we may express $A^N$ as a linear combination of the lower matrix powers of $A$:
$$
A^N = a_0 I + a_1 A + \ldots + a_{n-1} A^{n-1}.
$$
Therefore, all final states reachable in $N > n$ steps are also reachable in $n$ steps using a series of inputs $\{\bm{u}_k\}_0^{n-1}$. The state at step $n$ can be expressed as
$$
x_n = A^n x_0 + A^{n-1} B u_0 + A^{n-2} B u_1 + \ldots + B u_{n-1}
$$
which can be further manipulated into the form
$$
x_n = A^n x_0 + R \begin{bmatrix} u_0 \\ u_1 \\ \vdots \\ u_{n-1} \end{bmatrix}
$$
where
$$ 
R = \begin{bmatrix}
	B & AB & \dots & A^{n-1}B
\end{bmatrix},
$$
is the controllability matrix. Therefore, for the state $x_N = 0$ to be reachable from any $x_0 \in \Reals^n$ the controllability matrix $R$ has to be full rank. Similarly, all states $x_N \in \Reals^n$ are reachable from $x_0 = 0$ only if $R$ is full rank.

## Continuous-time

The state of a linear time-invariant system
$$
\dot{\bm{x}}(\tau) = \bm{A}\bm{x}(\tau) + \bm{B}\bm{u}(\tau), \quad \bm{x}(\tau) \in \Reals^n,\ \bm{u}(\tau) \in \Reals^m
$$ at time $t$, starting from the initial state $\bm{x}(0)$ and influenced by a continuous input $\bm{u}(\tau)$, can be expressed as
$$
\bm{x}(t) = e^{\bm{A}t} \bm{x}(0) + \int_0^t e^{\bm{A}(t-τ)} \bm{B} \bm{u}(τ)\ dτ. \tag{1}
$$
For square matrices that satisfy their own characteristic equation the Cayley-Hamilton theorem has a consequence that the exponential function $e^{\bm{A}t}$ can be expressed as
$$
e^{\bm{A}t} = ϕ_0(t) \bm{I} + ϕ_1(t) \bm{A} + \dots + ϕ_{n-1}(t) \bm{A}^{n-1}.
$$
After substituting it back into the second term of (1) we attain
$$
\bm{x}(t) = e^{\bm{A}t} \bm{x}(0) + \int_0^t \big( ϕ_0(t-τ)\, \bm{I} + ϕ_1(t-τ)\, \bm{A} + \dots + ϕ_{n-1}(t-τ)\, \bm{A}^{n-1} \big) \bm{B} \bm{u}(\tau) \, dτ
$$
which can be further manipulated into the form
$$
\bm{x}(t) = e^{\bm{A}t} \bm{x}(0) + \bm{\bm{R}}
\int_0^t
\begin{bmatrix}
	ϕ_0(t-τ)\ \bm{u}(τ)\\
	ϕ_1(t-τ)\ \bm{u}(τ)\\
	\vdots \\
	ϕ_{n-1}(t-τ)\ \bm{u}(τ)\\
\end{bmatrix}
dτ,
$$
where
$$ 
\bm{R} = \begin{bmatrix}
	\bm{B} & \bm{A}\bm{B} & \dots & \bm{A}^{n-1}\bm{B}
\end{bmatrix}
$$
is the controllability matrix. For the state $\bm{x}(t) = \bm{0}$ to be reachable from any $\bm{x}(0) \in \Reals^n$ the controllability matrix $\bm{R}$ has to be full rank. Similarly, all states $\bm{x}(t) \in \Reals^n$ are reachable from $\bm{x}(0) = \bm{0}$ only if $\bm{R}$ is full rank.
