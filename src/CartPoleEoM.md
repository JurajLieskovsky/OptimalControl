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
For generalized coordinates $q = \begin{bmatrix} s & \theta \end{bmatrix}^\top$ the system's kinetic and potential energy are
$$
\begin{aligned}
	T &= \frac{1}{2} \left( m_c \dot{s}^2 + m_p \left(\dot{x}_p^2 + \dot{y}_p^2\right) \right) \\
	V &= -g \, m_p \, \cos{(\theta)} ,
\end{aligned}
$$
where
$$
\begin{aligned}
	\dot{x}_p &= \dot{s} + l \, \dot{\theta} \, \cos(\theta) \\
	\dot{y}_p &= l \, \dot{\theta} \, \sin(\theta) .
\end{aligned}
$$
The individual terms of the manipulator equations[^1] are then
$$
\begin{aligned}
	M
	&=
	\begin{bmatrix}
		m_{c} + m_{p} & m_{p} \, l \cos{\left(\theta \right)} \\
		m_{p} \, l \cos{\left(\theta \right)} & m_{p} \, l^{2}
	\end{bmatrix}
	\\
	c &= \begin{bmatrix} -m_{p} \, l \sin{\left(\theta \right)} \, \dot{\theta}^{2} \\ 0 \end{bmatrix}
	\\
	\tau_g &= \begin{bmatrix} 0 \\ -g \, m_{p} \, l \sin{\left(\theta \right)}\end{bmatrix}
	\\
	B &= \begin{bmatrix}
		1 \\ 0
	\end{bmatrix} ,
\end{aligned}
$$
assuming a single input is acting in the direction of $s$.

## Linearization in the upright configuration

From the equations we may see that for the state and input vectors
$$
\begin{aligned}
x &= \begin{bmatrix} q \\ \dot{q} \end{bmatrix} = \begin{bmatrix} s & \theta & \dot{s} & \dot{\theta} \end{bmatrix}^\top \\
u &= \begin{bmatrix} u \end{bmatrix}
\end{aligned}
$$
all points
$$
\begin{aligned}
x^* &= \begin{bmatrix} q^{*} \\ \dot{q}^{*} \end{bmatrix} = \begin{bmatrix} s & \pi & 0 & 0 \end{bmatrix}^\top ,\quad s \in \mathbb{R} \\
u^* &= \begin{bmatrix} 0 \end{bmatrix}
\end{aligned}
$$
are stationary. In this configuration the relevant terms for the system's linearization are
$$
\begin{aligned}
M(q^*) &=	\begin{bmatrix}
	m_{c} + m_{p} & m_{p} \, l \\
	m_{p} \, l & m_{p} \, l^{2}
\end{bmatrix} \\
\frac{\partial \tau_g}{\partial q}(q^*) &= \begin{bmatrix} 0 & 0 \\ 0 & g \, m_{p} \, l \end{bmatrix} \\
\frac{\partial B}{\partial q}(q^*) &= 0 \\
B(q^*) &= \begin{bmatrix}
	1 \\ 0
\end{bmatrix} 
\end{aligned}
$$

---

[^1]: The python script for the derivation of the following terms can be found [here](https://github.com/lieskjur/CartPoleEoM). A very similar form of these equations of motion can also be found in section 3.2.1 of @@Underactuated2023. 
