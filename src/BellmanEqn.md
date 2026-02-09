# Bellman Equation
For a discrete-time linear system, with dynamics in the form
$$
x_{k+1} = f(x_k,u_k,k),
$$
let us assume we are trying to minimize the total cost
$$
J(x_0,u_{0:N-1},0) = \Phi(x_N) + \sum_{i=0}^{N-1} l(x_i,u_i,i).
$$
of a trajectory $(x_{0:N}, u_{0:N-1})$ where the initial state $x_0$ is prescribed. The concept of the total cost can be generalized for any $k \in [0 , N]$ to a *cost-to-go*
$$
J(x_k,u_{k:N-1},k) = \Phi(x_N) + \sum_{i=k}^{N-1} l(x_i,u_i,i),
$$
for which we may define a value function
$$
\begin{aligned}
V(x_k,k) = \min_{u_{k:N-1}} &\enspace J(x_k,u_{k:N-1},k) \\
\text{s.t.} &\enspace x_{i+1} = f(x_i,u_i,i) \quad \forall i \in [k, N-1]
\end{aligned}
$$
and an optimal control policy
$$
\begin{aligned}
u_{k:N-1}^* = \argmin_{u_{k:N-1}} &\enspace J(x_k,u_{k:N-1},k) \\
\text{s.t.} &\enspace x_{i+1} = f(x_i,u_i,i) \quad \forall i \in [k, N-1],
\end{aligned}
$$
the application of which results in the system following the optimal sequence of states $x_{k+1:N}^*$.

The so-called Bellman equation can then be derived by formulating the value function for step $k$ recursively, using the value function for step $k+1$. From its definition, it is apparent that
$$\tag{1}
V(x_k,k) = l(x_k,u_k^*,k) + V(x_{k+1}^*,k+1), \quad x_{k+1}^* = f(x_k, u_k^*, k),
$$
where
$$
V(x_N, N) = \Phi(x_N).
$$
Assuming we don't know what the optimal input at step $k$ is, we may pose the right-hand side of (1) as an optimization problem
$$\tag{2}
V(x_k,k) = \min_{u_k} \left(l(x_k,u_k,k) + V(f(x_k,u_k,k),k+1)\right).
$$
Equation (2) is then referred to as the Bellman equation.


