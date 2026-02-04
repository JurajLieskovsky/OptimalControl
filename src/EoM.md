# State-Space Representation of Mechanical Systems

## Equations of Motion
Let us consider *manipulator equations* in the form
$$
M(q) \ddot{q} + c(q,\dot{q}) - \tau_g(q) = B(q) u \tag{1}
$$
who's left-hand side may be for example derived from the system's kinetic $T(q,\dot{q})$ and potential $V(q)$ energy expressed in generalized coordinates by expanding Lagrange equations of the second kind
$$
\frac{\mathrm{d}}{\mathrm{d}t}\left(\frac{\partial L}{\partial \dot{q}}\right) - \frac{\partial L}{\partial q} = \sum_i \frac{\partial r_i}{\partial q} F_i,
$$
where $L = T-V$. First by separating the Lagrangian into its components
$$
\frac{\mathrm{d}}{\mathrm{d}t}\left(\frac{\partial T}{\partial \dot{q}} - \cancel{\frac{\partial V}{\partial \dot{q}}}\right) - \frac{\partial T}{\partial q} + \frac{\partial V}{\partial q} = \sum_i \frac{\partial r_i}{\partial q} F_i
$$
and then applying the change rule
$$
\frac{\partial^2 T}{\partial \dot{q}^2}\ddot{q} + \frac{\partial^2 T}{\partial \dot{q} \partial q} \dot{q} - \frac{\partial T}{\partial q} + \frac{\partial V}{\partial q} = \sum_i \frac{\partial r_i}{\partial q} F_i.
$$
If the external forces are linearly dependent on inputs $u_i$, such that $F_i = f_i u_i$, the terms of (1) as derived by this approach are
$$
\begin{aligned}
M(q) &= \frac{\partial^2 T}{\partial \dot{q}^2} \\
c(q,\dot{q}) &= \frac{\partial^2 T}{\partial \dot{q} \partial q} \dot{q} - \frac{\partial T}{\partial q} \\
\tau_g(q) &= - \frac{\partial V}{\partial q} \\
B(q) &= \begin{bmatrix} \frac{\partial r_1}{\partial q} f_1 & \ldots & \frac{\partial r_m}{\partial q} f_m \end{bmatrix}.
\end{aligned}
$$

## Continuous-time dynamics
Most commonly used state-space representation of a mechanical system in continuous time is attained by concatenating $q$ and $\dot{q}$ to form the system's state 
$$
x = \begin{bmatrix} q \\ \dot{q} \end{bmatrix} \,,\quad \dot{x} = f(x,u) = \begin{bmatrix} \dot{q} \\ M^{-1}(q) \left( \tau_g(q) - c(q,\dot{q}) + B(q) u \right) \end{bmatrix} \,.
$$

### Linearization
The system's dynamics can be linearized by performing a Taylor expansion around a point $\{x^*,u^*\}$ which yields
$$
\dot{x} = f(x, u) \approx f(x^*,u^*) + \underbrace{\frac{\partial f}{\partial x}(x^*,u^*)}_{A_C} \underbrace{(x - x^*)}_{\bar{x}} + \underbrace{\frac{\partial f}{\partial u}(x^*,u^*)}_{B_C} \underbrace{(u - u^*)}_{\bar{u}},
$$
where also $\dot{\bar{x}} = \frac{\mathrm{d}}{\mathrm{d}t}\left(x - x^*\right) = \dot{x}$.

If $\{x^*,u^*\}$ is a fixed point, i.e. $f(x^*,u^*) = 0$, first order partial derivatives of the system's dynamics simplify to
$$
\begin{aligned}
\frac{\partial f}{\partial x}(x^*,u^*) &= \begin{bmatrix} 0 & I \\ M^{-1}(q^*) \left( \frac{\partial \tau_g}{\partial q}(q^*) + \frac{\partial B}{\partial q}(q^*) \, u^* \right) & 0 \end{bmatrix} \\
\frac{\partial f}{\partial u}(x^*,u^*) &= \begin{bmatrix} 0 \\ M^{-1}(q^*) \, B(q^*) \end{bmatrix}
\end{aligned}
$$
as terms involving $\frac{\partial M^{-1}}{\partial q}$ drop out because $\tau_g - c + B u^* = 0$ for all fixed points. Partial derivatives of $c$ also disappear as all of its terms contain second degree products of velocities and all velocities must be equal to zero at a fixed point.

## Explicit Euler method discretization
The most basic approach with which we may discretize continuous-time dynamics of a nonlinear system is by integrating the systems state with a timestep of $h$ using the explicit Euler method
$$
x_{k+1} = x_k + h f(x_k,u_k) \,.
$$

### Linearization
Compared to more advanced integration methods, linearization of these discrete time dynamics around a point $\{x^*,u^*\}$ is trivial:
$$
\begin{aligned}
\underbrace{x_{k+1} - x^*}_{\bar{x}_{k+1}}&= x_k + h f(x_k, u_k) - x^* \\
&\approx h f(x^*,u^*) + \underbrace{\left( I + h \frac{\partial f}{\partial x}(x^*,u^*) \right)}_{A_D} \underbrace{(x_k - x^*)}_{\bar{x}_k} + \underbrace{h \frac{\partial f}{\partial u}(x^*,u^*)}_{B_D} \underbrace{(u_k - u^*)}_{\bar{u}_k} \,.
\end{aligned}
$$

