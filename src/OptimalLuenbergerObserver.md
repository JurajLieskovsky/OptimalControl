# Optimal Luenberger Observer

## Finite horizon
Let us consider a LTI system with additive Gaussian noise
$$
\begin{aligned}
x_k &= A x_{k-1} + B u_{k-1} + w_{k-1}, & Q_{k-1} &= \mathbb{E}[w_k w_k^\top] \\
y_k &= C x_k + v_k, & R_{k-1} &= \mathbb{E}[v_k v_k^\top].
\end{aligned}
$$
and a Luenberger observer
$$
\hat{x}_k = A \hat{x}_{k-1} + B u_{k-1} - L_k (C\hat{x}_{k-1} - y_{k-1}). \tag{1}
$$
The state estimate's error $e_k = \hat{x}_k - x_k$ and its covariance $P_k = \mathbb{E}[e_k e_k^\top]$ can be expressed recursively as
$$
\begin{aligned}
e_k &= w_{k-1} + (A - L_k C) e_{k-1} + L_k v_{k-1} \\
P_k &= Q_{k-1} + (A - L_k C) P_{k-1} (A - L_k C)^\top + L_k R_{k-1} L_k^\top. \tag{2}
\end{aligned}
$$
The gain $L_k$ can then be designed such that $P_k$ is minimized. This can be achieved by finding the stationary point $\frac{\partial P_k}{\partial L_k} = 0$, where
$$
L_k = P_{k-1} C^\top (C P_{k-1} C^\top + R_{k-1})^{-1}. \tag{3}
$$
Substituting (3) back into (2b) we attain the DDRE
$$
P_k = Q_{k-1} + A P_{k-1} A^\top − AP_{k-1}C^\top (C P_{k-1} C^\top + R_{k-1})^{-1} C P_{k-1} A^\top, \tag{4}
$$
which governs the evolution of the state error's covariance.

The state of the observer then consists of $\hat{x}_k$ and $P_k$, its dynamics described by (1) and (4). This observer can also be used in the case where the dynamics of the system are time variant.

## Infinite horizon

In the case where the covariances of the process and measurement noise are time-invariant, i.e.
$$
Q = \mathbb{E}[w_k w_k^\top], \quad R = \mathbb{E}[v_k v_k^\top],
$$
we can also design the gain of the observer based on the steady-state error covariance $P_k \rightarrow P$ at $k \rightarrow \infty$. The covariance $P$ can be obtained by solving the DARE
$$
P = Q + A P A^\top − APC^\top (C P C^\top + R)^{-1} C P A^\top, \tag{5}
$$
based on which we evaluate the gain
$$
L = P C^\top (C P C^\top + R)^{-1}.
$$

## Duality with LQR

It is of note that the form of (4) and (5) is identical to those of the [LQR](LQR-DT.md) with different matrices:

| LQR | Luenberger |
|-----|------------|
| $S$ |     $P$    |
| $A$ |  $A^\top$  |
| $B$ |  $C^\top$  |
