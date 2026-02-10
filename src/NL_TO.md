# Nonlinear Trajectory Optimization Problems

## Unconstrained Problems
Lets return to the unconstrained trajectory optimization problem
$$
\begin{aligned}
  \min_{x_{0:N}, u_{0:N-1}} & \quad \Phi(x_N) + \sum_{k=0}^{N-1} l(x_k, u_k, k) \\
  \text{s.t.} & \quad x_{k+1} = f(x_k, u_k, k), \quad \forall k \in \{0, \dots, N-1\} \\
              & \quad x_0 = \hat{x}_0 \\
\end{aligned}
$$
The simplest way to solve this problem is using sequential quadratic programming (SQP). As the name suggest the approach involves forming a sequence of quadratic programs. These programs have the same same structure as the [linear-quadratic problem](LQ_TO.md) which is achieved by evaluating Taylor expansions of cost functions (second-order) and the system's dynamics (first-order). If we consider a nominal trajectory $\bar{x}_{0:N}$, $\bar{u}_{0:N-1}$ (not necessarily dynamically feasible) we may linearize the system's dynamics along it
$$
\bar{x}_{k+1} + \delta x_{k+1} \approx f_k + f_{x_k} \delta x_k + f_{u_k} \delta u_k,
$$
where
$$
f_k = f(\bar{x}_k, \bar{u}_k, k)
,\quad
f_{x_k} = \frac{\partial f}{\partial x}(\bar{x}_k, \bar{u}_k, k)
,\quad
f_{u_k} = \frac{\partial f}{\partial u}(\bar{x}_k, \bar{u}_k, k)
$$
and also, using the same notation, create quadratic approximations of the final and running cost
$$
\begin{aligned}
\Phi(x_N) &\approx \Phi_N + \Phi_{x_N}^\top \delta x_N + \frac{1}{2} {\delta x_N}^\top \Phi_{xx_N} \delta x_N \\
l(x_k, u_k, k) &\approx l_k +
\begin{bmatrix} l_{x_k} \\ l_{u_k} \end{bmatrix}^\top \begin{bmatrix} \delta x_k \\ \delta u_k \end{bmatrix} +
\frac{1}{2} \begin{bmatrix} \delta x_k \\ \delta u_k \end{bmatrix}^\top \begin{bmatrix} l_{xx_k} & l_{xu_k} \\ l_{uu_k} & l_{uu_k} \end{bmatrix} \begin{bmatrix} \delta x_k \\ \delta u_k \end{bmatrix}.
\end{aligned}
$$
Provided an initial nominal trajectory the SQP algorithm repeatedly solves the problem
$$
\begin{aligned}
  \tag{2a-c}
  \min_{\substack{\delta x_{0:N} \\ \delta u_{0:N-1}}} & \quad \Phi_{x_N}^\top \, \delta x_N + \frac{1}{2} {\delta x_N}^\top \Phi_{xx_N} \delta x_N + \sum_{k=0}^{N-1} \left(
    \begin{bmatrix} l_{x_k} \\ l_{u_k} \end{bmatrix}^\top \begin{bmatrix} x_k \\ u_k \end{bmatrix} +
    \frac{1}{2} \begin{bmatrix} \delta x_k \\ \delta u_k \end{bmatrix}^\top \begin{bmatrix} l_{xx_k} & l_{xu_k} \\ l_{uu_k} & l_{uu_k} \end{bmatrix} \begin{bmatrix} \delta x_k \\ \delta u_k \end{bmatrix} \right) \\
  \text{s.t.} & \quad \delta x_{k+1} = A_k \delta x_k + B_k \delta u_k + f_k - \bar{x}_{k+1}, \quad \forall k \in \{0, \dots, N-1\} \\
              & \quad \delta x_0 = \hat{x}_0 - \bar{x}_0,
\end{aligned}
$$
producing an update $\delta x_{0:N}$, $\delta u_{0:N-1}$ to the nominal trajectory in a manor that is not dissimilar to the Newton method for unconstrained optimization. Ideally the nominal trajectory can be updated at every iteration using
$$
\begin{aligned}
  \bar{x}_k &\leftarrow \bar{x}_k + \delta x_k \\
  \bar{u}_k &\leftarrow \bar{u}_k + \delta u_k
\end{aligned}
$$
but typically *line-search* strategies must be used. Also the quadratic problem is not necessarily convex in which case it must be *regularized*. The problem (2) itself has the same exact form of the [unconstrained linear-quadratic problem](LQ_TO.md#unconstrained-problems) we previously described so once line-search and regularization are handled, we can use the same exact techniques.

## Constrained Problems

Similarly to how we linearized the system's dynamics it is common to also linearize additional constraints, e.g.
$$
\begin{aligned}
g(x_k, u_k, k) &\leq 0\\
h(x_k, u_k, k) &= 0.
\end{aligned}
$$
However, for some types of constraints, such as second-order cones, there are specialized ways in which they can be effectively handled (see ADMM).

Due to the special structure of the trajectory optimization problem, many specialized solvers capable of handling additional constraints exist. As nonlinear MPC is still extremely computationally demanding these solvers are tailored to handle specific types of constraints, also making deliberate choices when it comes to how the algorithms converge ([Altro](https://github.com/RoboticExplorationLab/ALTRO.jl), [Crocoddyl](https://github.com/loco-3d/crocoddyl), [MJPC](https://github.com/google-deepmind/mujoco_mpc)).
