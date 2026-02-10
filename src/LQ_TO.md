# Linear Quadratic Trajectory Optimization Problems

## Unconstrained Problems

Let us start by addressing the case where dynamics of our system are linear and the cost functions quadratic
$$
\begin{aligned}
  \tag{2a-c}
  \min_{x_{0:N}, u_{0:N-1}} & \quad q_N^\top \, x_N + \frac{1}{2} x_N^\top Q_N x_N + \sum_{k=0}^{N-1} \left(
    \begin{bmatrix} q_k \\ r_k \end{bmatrix}^\top \begin{bmatrix} x_k \\ u_k \end{bmatrix} +
    \frac{1}{2} \begin{bmatrix} x_k \\ u_k \end{bmatrix}^\top \begin{bmatrix} Q_k & S_k^\top \\ S_k & R_k \end{bmatrix} \begin{bmatrix} x_k \\ u_k \end{bmatrix} \right) \\
  \text{s.t.} & \quad x_{k+1} = A_k x_k + B_k u_k + c_k, \quad k = 0, \ldots, N-1 \\
              & \quad x_0 = \hat{x}_0
\end{aligned}
$$
This problem is very similar to that of finite-horizon LQR. In fact, it differs only in the inclusion of the cross term $S_k$, which can also be easily incorporated into LQR and linear terms $q_k$ and $r_k$ which can be accounted for in LQR if one considers the value function in the form $V(x_k,k) = p_k^\top x_k + x_k^\top P_k x_k$. Also there is an additional term $c_k$ who's utility we will show later, when discussing nonlinear trajectory optimization.

There are a few approach that can be used to solve this problem which differ mostly in their algorithmic complexity based on how the sparse structure of optimization problem is exploited.

### Condensing

One way to exploit the block sparse structure is to eliminate states $x_{0:N}$ from the problem's decision variables. As the constraint (2b) corresponds to the evolution of a linear time-varying system, states $x_{0:N}$ are fully determined by inputs $u_{0:N-1}$ and the initial state $\hat{x}_0$
$$
\begin{aligned}
  x_0 &= \hat{x}_0 \\
  x_1 &= A_0 \hat{x}_0 + B_0 u_0 + c_0 \\
  x_2 &= A_1 A_0 \hat{x}_0 + A_1 (B_0 u_0 + c_0) + (B_1 u_1 + c_1) \\
      &\enspace\vdots \\
  x_N &= \prod_{\mathclap{k=N-1}}^0 A_k \hat{x}_0 + \prod_{\mathclap{k=N-1}}^1 A_k (B_0 u_0 + c_0) + \prod_{\mathclap{k=N-1}}^2 A_k (B_1 u_1 + c_1) + \ldots + (B_{N-1} u_{N-1} + c_{N-1}).
\end{aligned}
$$
As a consequence of these eliminations, the resulting optimization problem is unconstrained and the matrix (of the quadratic term) in the objective function is dense. The algorithmic complexity of condensing is typically $\mathcal{O}(N^3 n_u^3)$.

### Solving the KKT system

Another way to exploit the sparse structure is to solve the problem's KKT conditions
$$
\begin{bmatrix}
     & -I  &           &          &          \\
  -I & Q_0 & S_0^\top  & A_0^\top &          \\
     & S_0 & R_0       & B_0^\top &          \\
     & A_0 & B_0       &          &          \\
     &     &           &          & \ddots   & -I \\
     &     &           &          & -I       & Q_{N-1} & S_{N-1}^\top  & A_{N-1}^\top & \\
     &     &           &          &          & S_{N-1} & R_{N-1}       & B_{N-1}^\top & \\
     &     &           &          &          & A_{N-1} & B_{N-1}       &              & -I\\
     &     &           &          &          &         &               & -I           & Q_N
\end{bmatrix}
\begin{bmatrix}
  \lambda_0 \\
  x_0 \\
  u_0 \\
  \vdots \\
  \lambda_{N-1} \\
  x_{N-1} \\
  u_{N-1} \\
  \lambda_N \\
  x_N
\end{bmatrix}
= -
\begin{bmatrix}
\hat{x}_0 \\
q_0 \\
r_0 \\
c_0 \\
\vdots \\
q_{N-1} \\
r_{N-1} \\
c_{N-1} \\
q_N
\end{bmatrix}
$$

either using sparse linear algebra routines or by manual factorizations. In both cases the algorithmic complexity of $\mathcal{O}(N (n_x + n_u)^3)$ can be achieved.  

#### Riccati recursion

Riccati recursion is a process of factorizing the system of KKT conditions. If we consider the KKT conditions 
$$
\begin{bmatrix}
  \ddots       &  -I      \\
  -I           & Q_k  & S_k^\top  & A_k^\top & \\
               & S_k  & R_k       & B_k^\top & \\
               & A_k  & B_k       &              & -I\\
               &          &               & -I           & P_{k+1}
\end{bmatrix}
\begin{bmatrix}
  \lambda_k \\
  x_k \\
  u_k \\
  \lambda_{k+1} \\
  x_{k+1}
\end{bmatrix}
= -
\begin{bmatrix}
c_{k-1} \\
q_k \\
r_k \\
c_k \\
p_{k+1}
\end{bmatrix}
$$
we can step-by-step condense them into the form
$$
\begin{bmatrix}
  \ddots       &  -I \\
  -I           & P_k \\
\end{bmatrix}
\begin{bmatrix}
  \lambda_k \\
  x_k \\
\end{bmatrix}
= -
\begin{bmatrix}
c_{k-1} \\
p_k
\end{bmatrix}
$$
where
$$
\begin{aligned}
\tag{3a-b}
P_k &= Q_k + A_k^\top P_{k+1} A_k - (S_k + B_k^\top P_{k+1} A_k)^\top (R_k + B_k^\top P_{k+1} B_k)^{-1} (S_k + B_k^\top P_{k+1} A_k) \\
p_k &= q_k + A_k^\top (p_{k+1} + P_{k+1} c_k) \\ & \quad - (S_k + B_k^\top P_{k+1} A_k)^\top (R_k + B_k^\top P_{k+1} B_k)^{-1} (r_k + B_k^\top (p_{k+1} + P_{k+1} c_k)).
\end{aligned}
$$
To tackle the KKT system as a whole we start by setting
$$
k = N-1, \quad P_{k+1} = Q_N, \quad p_{k+1} = q_N
$$
and traversing the horizon backwards to $k=0$. The optimal inputs $u_k^*$ are given as an affine function of $x_k$
$$
\begin{aligned}
\tag{4}
u_k^* &= -(R_k + B_k^\top P_{k+1} B_k)^{-1} (r_k + B_k^\top (p_{k+1} + P_{k+1} c_k)) \\ &\quad - (R_k + B_k^\top P_{k+1} B_k)^{-1} (S_k + B_k^\top P_{k+1} A_k) x_k.
\end{aligned}
$$

The name "Riccati recursion" is not incidental. In fact there is a close relationship between the factorization process we have just described and obtaining the optimal control using [discrete-time finite-horizon LQR](LQR-DT-FH). First of all, terms $P_k$ and $p_k$ can be used to form the *value function*
$$
V(x_k,k) = p_k^\top x_k + x_k^\top P_k x_k.
$$
Then if we look at (3a) we can see that it differs from the *discrete-time dynamics Riccati equation* only in the inclusion of the cross term $S_k$. In fact if we were to include terms $q_k$, $r_k$, $S_k$, $c_k$ in the problem when deriving DT-FH-LQR, we would also have terms $p_k$ and $P_k$ given by (3) and the optimal control input would take the form of (4).

The full derivation of the Riccati recursion is located [here](RiccatiRecursion.md).

## Constrained Problems

In addition to (2b-c) we may also add other affine equality/inequality constraints, such as
$$
\begin{gathered}
x_N = \hat{x}_N \\
u_{\min} \leq u_k \leq u_{\max} \\
G_{x_k} x_k + G_{u_k} u_k \geq -g_k
,
\end{gathered}
$$
at which point the problem is still classified as a quadratic program. In this case, without the knowledge of constrained optimization method, we can either use [optimization modeling languages](OptimizationModelingLanguages.md) or [use sparse solvers for QP](MPC-Direct.md). Alternatively, if constraint optimization methods are applied, they generally form a sequence of problems similar to (2) which can be solved using the Riccati recursion.
