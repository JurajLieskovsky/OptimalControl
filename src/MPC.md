Model predictive control (MPC) is a control strategy which relies on the system's model to predict and optimize its trajectory. This is done repeatedly to form a feedback loop. *Trajectory optimization* therefore lies as the heart of MPC. Typically the optimization problems are solved using gradient based methods which guarantees that the globally optimal solution is found only if the problem is convex. For nonconvex problems we have to settle for local minima. In this case, the initial estimate of the solution determines which local minimum is found.

We will focus on solving the trajectory optimization problem in discrete time. That is not to say that continuous-time formulations do not exist. For example, *collocation* methods for trajectory optimization are a well research field. However, the transcription produces an optimization problem differing only in additional "algebraic" decision variables @@Diehl2009.

The basic unconstrained trajectory optimization problem takes the form
$$
\begin{aligned}
  \tag{1a-c}
  \min_{x_{0:N}, u_{0:N-1}} & \quad \Phi(x_N) + \sum_{k=0}^{N-1} l(x_k, u_k, k) \\
  \text{s.t.} & \quad x_{k+1} = f(x_k, u_k, k), \quad k = 0, \ldots, N-1 \\
              & \quad x_0 = \hat{x}_0 \\
\end{aligned}
$$
where $\Phi$ is the final cost, $l$ the running cost, $f$ are the system's dynamics, and $\hat{x}_0$ is the initial state. In addition to constraints (2b-c) we may include additional constraints such as
- equality
  $$ h(x_k, u_k, k) = 0 $$
  $$ x_N = \hat{x}_N $$
- inequality
  $$ g(x_k, u_k, k) \leq 0 $$
- box
  $$ x_{\min} \leq x \leq x_{\max} $$
  $$ u_{\min} \leq u \leq u_{\max} $$
- second-order cone
- ...

The decision of which constraints are included should not be made only based on problem at hand but also the solver/method we want to use.
