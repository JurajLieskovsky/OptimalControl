# Bi-Rotor with Payload

For generalized coordinates $q = \begin{bmatrix} y & z & \theta & \phi \end{bmatrix}^\top$ the system's kinetic and potential energy are
$$
\begin{aligned}
  T &= \frac{1}{2}\left(m_Q (\dot{y}^2 + \dot{z}^2) + I_Q \dot{\theta}^2 + m_P (\dot{y}_P^2 + \dot{z}_P^2)\right) \\
  V &= g \, m_Q \, z + g \, m_P (z - l \cos(\phi))
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
M &= \begin{bmatrix}
	m_Q + m_P & 0 & 0 & l \, m_P \cos{(\phi)} \\
	0 & m_Q + m_P & 0 & l \, m_P \sin(\phi) \\
	0 & 0 & I_Q & 0 \\
	l \, m_P \cos(\phi) & l \, m_P \sin(\phi) & 0 & l^{2} m_P
\end{bmatrix}
\\
c &= \begin{bmatrix}
	- l \, m_P \sin(\phi) \, \dot{\phi}^2 \\
	l \, m_P \cos(\phi) \, \dot{\phi}^2 \\
	0 \\
	0
\end{bmatrix}
\\
\tau_p &= \begin{bmatrix}
	0 \\
	-g (m_P + m_Q) \\
	0 \\
	-g \, l \, m_P \sin(\phi)
\end{bmatrix}
\\
B &= \begin{bmatrix}
	-\sin{(\theta)} & - \sin{(\theta)}\\\cos{(\theta)} & \cos{(\theta)}\\- a & a\\0 & 0
\end{bmatrix}
\end{aligned}
$$
