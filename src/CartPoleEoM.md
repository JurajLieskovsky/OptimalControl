# Cart-Pole Equations of Motion
```
                  \
                  /\
                 /  \
                /    \
               l      \
              /       >< m_p
             /       //
            /       //
          \/       //
           \      //
            \    //
  |   |------\--//------|
  |   |       \//\      |
  g   |  m_c  ( ) theta |
  |   |        |_/      |
  v   |========|========|
_________ooo___|___ooo_________
               |
//|-----s----->|
```

Equations of motion of a cart-pole can be derived using the expanded form of Lagrange's equations of the second kind
$$
\underbrace{
\frac{\partial^2 T}{\partial \bm{\dot{q}}^2}
}_{\bm{M}(\bm{q})} \bm{\ddot{q}}
+
\underbrace{
\frac{\partial^2 T}{\partial \bm{\dot{q}} \partial \bm{q}} \bm{\dot{q}} - \frac{\partial T}{\partial \bm{q}}
}_{\bm{c}(\bm{q}, \dot{\bm{q}})}
+
\underbrace{
\frac{\partial V}{\partial \bm{q}}
}_{-\bm{\tau}_p(\bm{q})}
= \bm{\tau} \,,
$$
where $\bm{q} = \begin{bmatrix} s & \theta \end{bmatrix}^\top$ are generalized coordinates and $T$ and $V$ are the system's kinetic and potential energy
$$
\begin{aligned}
	T &= \frac{1}{2} \left( m_c \dot{s}^2 + m_p \left(\dot{x}_p^2 + \dot{y}_p^2\right) \right) \\
	V &= g \, m_p \, \cos{(\theta)} \,,
\end{aligned}
$$
where
$$
\begin{aligned}
	\dot{x}_p &= \dot{s} + l \, \dot{\theta} \, \cos(\theta) \\
	\dot{y}_p &= l \, \dot{\theta} \, \sin(\theta) \,.
\end{aligned}
$$
The individual terms of the equations of motion for this system are then
$$
\begin{aligned}
	\bm{M}
	&=
	\begin{bmatrix}
		m_{c} + m_{p} & m_{p} \, l \cos{\left(\theta \right)} \\
		m_{p} \, l \cos{\left(\theta \right)} & m_{p} \, l^{2}
	\end{bmatrix}
	\\
	\bm{c} &= \begin{bmatrix} m_{p} \, l \sin{\left(\theta \right)} \, \dot{\theta}^{2} \\ 0 \end{bmatrix}
	\\
	\bm{\tau}_p &= \begin{bmatrix} 0 \\ g \, m_{p} \, l \sin{\left(\theta \right)}\end{bmatrix}
	\\
	\bm{\tau} &= \begin{bmatrix}
		u \\ 0
	\end{bmatrix} \,.
\end{aligned}
$$

Consequently, we may form the state-space representation of our system $\dot{\bm{x}} = \bm{f}_{\textrm{c}}(\bm{x},\bm{u})$ for the state and input vectors
$$
\bm{x} = \begin{bmatrix} \bm{q} \\ \dot{\bm{q}} \end{bmatrix}
\,,\quad
\bm{u} = \begin{bmatrix} u \end{bmatrix}
$$
as
$$
\dot{\bm{x}} =
\begin{bmatrix}
	\dot{\bm{q}} \\
	\bm{M}^{-1}(\bm{q}) \left(-\bm{c}(\bm{q}, \dot{\bm{q}})+\bm{\tau}_p(\bm{q})+\bm{\tau}(\bm{q},u)\right)
\end{bmatrix}
\,,
$$

---

[Link](https://github.com/CVUT-FS-12110/CartPoleEoM) to the sympy script for symbolically deriving the terms.
