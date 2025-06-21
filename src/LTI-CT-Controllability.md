# Controlability of LTI Continuous-Time Systems

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

