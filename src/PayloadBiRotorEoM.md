# Bi-Rotor with Payload

For generalized coordinates $q = \begin{bmatrix} y & z & \theta & \phi \end{bmatrix}^\top$ the system's kinetic and potential energy are
$$
\begin{aligned}
  T &= \frac{1}{2}\left(m_Q (\dot{y}^2 + \dot{z}^2) + I_Q \dot{\theta}^2 + m_P (\dot{y}_P^2 + \dot{z}_P^2)\right) \\
  V &= g \, m_Q \, y + g \, m_P (y - l \cos(\phi))
\end{aligned}
$$
where
$$
\dot{y}_P = \dot{y} + l \, \dot{\phi} \cos(\phi)
,\quad
\dot{z}_P = \dot{z} + l \, \dot{\phi} \sin(\phi).
$$
The two forces acting on the system and their action arms are
$$
F_{1,2} = u_{1,2} \begin{bmatrix} -\sin(\theta) \\ \cos(\theta) \end{bmatrix}
,\quad
r_{1,2} = \begin{bmatrix} y \mp a \cos(\theta) \\ z \mp a \sin(\theta) \end{bmatrix}.
$$
The individual terms of the manipulator equations are then
$$
\begin{aligned}
	M
	&=
	\begin{bmatrix}
	\end{bmatrix}
	\\
	c &= \begin{bmatrix}\end{bmatrix}
	\\
	\tau_g &= \begin{bmatrix}\end{bmatrix}
	\\
	B &= \begin{bmatrix}\end{bmatrix},
\end{aligned}
$$


