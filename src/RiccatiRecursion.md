To illustrate the process, let us consider the KKT conditions
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
\end{bmatrix}.
$$
Using the last row we can express $x_{k+1}$ as
$$
x_{k+1} = P_{k+1}^{-1} \lambda_{k+1} - P_{k+1}^{-1} \, p_{k+1}  
$$
and consequently eliminate it from the KKT system
$$
\begin{bmatrix}
  \ddots       &  -I      \\
  -I           & Q_k  & S_k^\top  & A_k^\top \\
               & S_k  & R_k       & B_k^\top \\
               & A_k  & B_k       & -P_{k+1}^{-1}     \\
\end{bmatrix}
\begin{bmatrix}
  \lambda_k \\
  x_k \\
  u_k \\
  \lambda_{k+1} \\
\end{bmatrix}
= -
\begin{bmatrix}
c_{k-1} \\
q_k \\
r_k \\
c_k + P_{k+1}^{-1} \, p_{k+1}
\end{bmatrix}.
$$
In a similar fashion we may eliminate
$$
\lambda_{k+1} = P_{k+1} (A_k x_k + B_k u_k) + P_{k+1} c_k + p_{k+1},
$$
attaining
$$
\begin{bmatrix}
  \ddots       &  -I      \\
  -I           & \bar{Q}_k & \bar{S}_k^\top \\
               & \bar{S}_k & \bar{R}_k \\
\end{bmatrix}
\begin{bmatrix}
  \lambda_k \\
  x_k \\
  u_k \\
\end{bmatrix}
= -
\begin{bmatrix}
c_{k-1} \\
\bar{q}_k \\
\bar{r}_k
\end{bmatrix}
$$
where
$$
\begin{aligned}
  \bar{Q}_k &= Q_k + A_k^\top P_{k+1} A_k \\
  \bar{S}_k &= S_k + B_k^\top P_{k+1} A_k \\
  \bar{R}_K &= R_k + B_k^\top P_{k+1} B_k \\
  \bar{q}_k &= q_k + A_k^\top (p_{k+1} + P_{k+1} c_k) \\
  \bar{r}_k &= r_k + B_k^\top (p_{k+1} + P_{k+1} c_k).
\end{aligned}
$$
Finally, we may also eliminate
$$
u_k = -\bar{R}_k^{-1} \bar{r}_k -\bar{R}_k^{-1} \bar{S}_k x_k 
$$
to attain 
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
P_k &= \bar{Q}_k - \bar{S}_k^\top \bar{R}_k^{-1} \bar{S}_k \\
p_k &= \bar{q}_k - \bar{S}_k^\top \bar{R}_k^{-1} \bar{r}_k.
\end{aligned}
$$
This process can be repeated for $k \leftarrow k-1$.

