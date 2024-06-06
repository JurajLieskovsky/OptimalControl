# Discretization of LTI Systems

Let us consider a linear time-invariant system in the form
$$
\dot{x}(\tau) = A x(\tau) + B u(\tau) \,.
$$
<!--
We assume the solution of the integral
$$
x(t) = \int_{0}^{t} A x(\tau) + B u(\tau) \ d\tau
$$
to be in the general form
$$
x(t) = e^{At} z(t) \,. \tag{2}
$$
By substituting (2) into (1) and holding the result equal to (1) differentiated in time we get
$$
\begin{aligned}
A e^{At} z(t) + B u(t) &= A e^{At} z(t) + e^{At}\dot{z}(t) \\
B u(t) &= e^{At} \dot{z}(t) 
\end{aligned}
$$
-->
Integration of the system's dynamics over an iterval $\tau \in \langle 0, t+h \rangle$ gives us
$$
x(t+h) = e^{A(t+h)}x(0) + \int_0^{t+h} e^{A(t+h-\tau)}Bu(\tau) \ d\tau \,.
$$
To express its state at $x(t+h)$ with respect to the state $x(t)$ we may perform a series of manipulations
$$
\begin{aligned}
x(t+h) &= e^{A(t+h)}x(0) + \int_0^{t+h} e^{A(t+h-\tau)}Bu(\tau) \ d\tau \\
&= e^{A(t+h)}x(0) + \int_0^{t} e^{A(t+h-\tau)}Bu(\tau) \ d\tau + \int_t^{t+h} e^{A(t+h-\tau)}Bu(\tau) \ d\tau \\
&= e^{Ah} \underbrace{\left(e^{At}x(0) + \int_0^{t} e^{A(t-\tau)}Bu(\tau) \ d\tau \right)}_{x(t)} + \int_t^{t+h} e^{A(t+h-\tau)}Bu(\tau) \ d\tau \,.
\end{aligned} \tag{1}
$$
If we then set $u(\tau) = \hat{u}$, $\tau \in \langle t, t+h)$ the integral
$$
\int_t^{t+h} e^{A(t+h-\tau)}Bu(\tau) \ d\tau
$$
can be manipulated into
$$
\begin{aligned}
\int_t^{t+h} e^{A(t+h-\tau)}Bu(\tau) \ d\tau &= e^{A(t+h)}\int_t^{t+h} e^{-A\tau} \ d\tau \, B\hat{u} \\
 &= e^{A(t+h)}\left[ -A^{-1}e^{-A\tau}\right]_t^{t+h} \, B\hat{u} \\
 &= e^{A(t+h)} \left( -A^{-1} e^{-A(t+h)} + A^{-1}e^{-At}\right) B\hat{u}\\
 &= A^{-1}\left(e^{Ah} - I\right) B\hat{u} \,.
\end{aligned} \tag{2}
$$
By substituting (2) into (1) we obtain
$$
x_{k+1} = e^{Ah} x_k + A^{-1}(e^{Ah} - I) \, Bu_k \tag{3}
$$
where $x_{k+1} = x(t+h)$, $x_k = x(t)$, and $u_k = \hat{u}$. 

---

If we use the first two terms of the taylor expansion
$$
e^{Ah} = I + Ah + \frac{(Ah)^2}{2!} + \ldots
$$
in (3) we get the system representation
$$
x_{k+1} = (I + Ah) x_k + Bhu_k \,.
$$
