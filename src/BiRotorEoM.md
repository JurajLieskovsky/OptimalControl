# Bi-Rotor Equations of Motion

As a bi-rotor (quadcopter simplified to 2D) is essentially a rigid body, its equations of motion can be easily derived as
$$
\begin{aligned}
m \ddot{x} &= -\sin(\theta) \left( u_1 + u_2 \right) \\
m \ddot{y} &= \cos(\theta) \left( u_1 + u_2 \right) - mg\\
I \ddot{\theta} &= r \left( u_1 - u_2 \right) \,.
\end{aligned}
$$

## Linearization in hovering configuration

From the EoM we may see that for the state and input vectors
$$
\begin{aligned}
\bm{x} &= \begin{bmatrix} \bm{q} \\ \dot{\bm{q}} \end{bmatrix} = \begin{bmatrix} x & y & \theta & \dot{x} & \dot{y} & \dot{\theta} \end{bmatrix}^\top \\
\bm{u} &= \begin{bmatrix} u_1 & u_2 \end{bmatrix}^\top
\end{aligned}
$$
all points
$$
\begin{aligned}
\bm{x}^* &= \begin{bmatrix} \bm{q}^{*} \\ \dot{\bm{q}}^{*} \end{bmatrix} = \begin{bmatrix} x & y & 0 & 0 & 0 & 0 \end{bmatrix}^\top \,,\quad \{x,y\} \in \mathbb{R}^2 \\
\bm{u}^* &= \begin{bmatrix} \frac{1}{2}mg & \frac{1}{2}mg \end{bmatrix}^\top \\
\end{aligned}
$$
are stationary points, for which the linearization of EoM is also trivial
$$
\begin{aligned}
m\ddot{x} &\approx -mg\,\theta \\
m\ddot{y} &\approx \bar{u}_1 + \bar{u}_2 \\
I\ddot{\theta} &\approx r (\bar{u}_1 - \bar{u}_2) \,,
\end{aligned}
$$
where $\bar{u}_i = u_i - \frac{1}{2}mg$ from which we may derive

## Derivation in manipulator equation form

For those who want to validate the equations by deriving the manipulator equations, kinetic and potential energy for generalized coordinates
$$
\bm{q} = \begin{bmatrix}
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
\bm{M} = \begin{bmatrix}
  m & 0 & 0 \\
  0 & m & 0 \\
  0 & 0 & I
\end{bmatrix} \quad
\bm{c} = \begin{bmatrix} 0 \\ 0 \\ 0 \end{bmatrix} \quad
\bm{\tau}_g = \begin{bmatrix} 0 \\ -mg \\ 0 \end{bmatrix} \,.
$$
The manipulation matrix
$$
\bm{B} = \begin{bmatrix} -\sin(\theta) & -\sin(\theta) \\ \cos(\theta) & \cos(\theta) \\ r & -r \end{bmatrix}
$$
can then be derived separately by evaluating thrust vectors and differentiating moment arms.



