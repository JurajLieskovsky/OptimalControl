# Bi-Rotor Equations of Motion

As a bi-rotor (quadcopter simplified to 2D) is essentially a rigid body, its equations of motion can be easily derived as
$$
\begin{aligned}
m \ddot{x} &= -\sin(\theta) \left( u_1 + u_2 \right) \\
m \ddot{y} &= \cos(\theta) \left( u_1 + u_2 \right) - mg \\
I \ddot{\theta} &= a \left( u_1 - u_2 \right) \,.
\end{aligned}
$$

## Linearization in a hovering configuration

From the EoM we may see that for the state description
$$
\begin{aligned}
x &= \begin{bmatrix} x \\ y \\ \theta \\ \dot{x} \\ \dot{y} \\ \dot{\theta} \end{bmatrix}, &
\dot{x} &= \begin{bmatrix}
\dot{x} \\
\dot{y} \\
\dot{\theta} \\
-\frac{1}{m} \sin(\theta) \left( u_1 + u_2 \right) \\
\frac{1}{m} \cos(\theta) \left( u_1 + u_2 \right) - mg \\
\frac{a}{I} \left( u_1 - u_2 \right)
\end{bmatrix} \\  
u &= \begin{bmatrix} u_1 \\ u_2 \end{bmatrix}
\end{aligned}
$$
all points
$$
\begin{aligned}
x^* &= \begin{bmatrix} x & y & 0 & 0 & 0 & 0 \end{bmatrix}^\top \,,\quad \{x,y\} \in \mathbb{R}^2 \\
u^* &= \begin{bmatrix} \frac{1}{2}mg & \frac{1}{2}mg \end{bmatrix}^\top \\
\end{aligned}
$$
are stationary points, for which the system's linearization is trivial
$$
\begin{aligned}
	A &= \left[\begin{array}{ccc|ccc}
		     &     &     &  1  &     &     \\
		     &     &     &     &  1  &     \\
		     &     &     &     &     &  1  \\ \hline
		     &     & -g  &     &     &     \\
		     &     &     &     &     &     \\
		     &     &     &     &     &    
	\end{array}\right]
  \\
	B &= \left[\begin{array}{cc}
		            &              \\
		            &              \\
		            &              \\ \hline
		            &              \\
		\frac{1}{m} & \frac{1}{m}  \\
		\frac{a}{I} & \frac{-a}{I}
	\end{array}\right]
\end{aligned}
$$

## Derivation in manipulator equation form

For those who want to validate the equations by deriving the manipulator equations, kinetic and potential energy for generalized coordinates
$$
q = \begin{bmatrix}
  x \\ y \\ \theta
\end{bmatrix}
$$
are 
$$
\begin{aligned}
T &= \frac{1}{2} m (\dot{x}^2 + \dot{y}^2) + \frac{1}{2} I \dot{\theta}^2 \\
V &= m g y
\end{aligned}
$$
which should yield
$$
M = \begin{bmatrix}
  m & 0 & 0 \\
  0 & m & 0 \\
  0 & 0 & I
\end{bmatrix} \quad
c = \begin{bmatrix} 0 \\ 0 \\ 0 \end{bmatrix} \quad
\tau_g = \begin{bmatrix} 0 \\ -mg \\ 0 \end{bmatrix} \,.
$$
The manipulation matrix
$$
B = \begin{bmatrix} -\sin(\theta) & -\sin(\theta) \\ \cos(\theta) & \cos(\theta) \\ a & -a \end{bmatrix}
$$
can then be derived separately by evaluating thrust vectors and differentiating moment arms.
