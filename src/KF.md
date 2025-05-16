# Kalman Filter

Let us consider a LTI system with additive Gaussian noise
$$
\begin{aligned}
x_k &= A x_{k-1} + B u_{k-1} + w_{k-1}, & Q_k &= \mathbb{E}[w_k w_k^\top] \\
y_k &= C x_k + v_k, & R_k &= \mathbb{E}[v_k v_k^\top].
\end{aligned}
$$
In addition to the state estimate $\hat{x}_k$ the state of the Kalman Filter includes the error covariance
$$
P_k = \mathbb{E}[e_k e_k^\top],
$$
where $e_k = \hat{x}_k - x_k$ is the state estimate's error.

The Kalman filter estimates the state $x_k$ in two steps, first creating an *a priori* state estimate and error covariance
$$
\begin{aligned}
\hat{x}_{k|k-1} &= A \hat{x}_{k-1} + B u_{k-1} \\
P_{k|k-1} &= A P_{k-1} A^\top + Q_{k-1},
\end{aligned}
$$
where
$$
P_{k|k-1} = \mathbb{E}[e_{k|k-1} e_{k|k-1}^\top], \quad
e_{k|k-1} = \hat{x}_{k|k-1} - x_k = A e_{k-1} - w_{k-1},
$$
and then performing a correction based on the measurement $y_k$ and *Kalman gain* $L_k$, to attain the *a posteriori* state estimate and error covariance
$$
\begin{aligned}
\hat{x}_k &= \hat{x}_{k|k-1} - L_k (C \hat{x}_{k|k-1} - y_k) \\
P_k &= (I - L_k C) P_{k|k-1} (I - L_k C)^\top + L_k R_k L_k^\top, \tag{1}
\end{aligned}
$$
as
$$
e_k = \hat{x}_k - x_k = (I - L_k C) e_{k|k-1} + L_k v_k.
$$
The Kalman gain is designed to minimize the a posteriori error covariance by finding the stationary point of (1b)
$$
L_k = P_{k|k-1} C^\top S_k^{-1}, \quad S_k = C P_{k|k-1} C^\top + R_k. \tag{2}
$$
After substituting (2) into (1b) we can manipulate the equation into the "Joseph" form
$$
P_k = P_{k|k-1} - L_k S_k L_k^\top,
$$
or alternatively the simplified form
$$
P_k = (I - L_k C) P_{k|k-1},
$$
which is numerically less stable.

