# Bellman Equation
Let us assume we are trying to minimize the *total cost*
$$
J(\bm{x}_0,\{\bm{u}_i\}_{i=0}^{N-1},0,N) = \Phi(\bm{x}_N,N) + \sum_{i=0}^{N-1} \mathcal{L}(\bm{x}_i,\bm{u}_i).
$$
of a discrete-time system's trajectory $\{\bm{x}_i\}_{i=0}^N$ with dynamics in the form
$$
x_{k+1} = \bm{f}(\bm{x}_k,\bm{u}_k) ,
$$
starting from the state $\bm{x}_0 = \tilde{\bm{x}}_0$.

The concept of the total cost can be generalized for any $k \in \langle 0 , N \rangle$ to a *cost-to-go*
$$
J(\bm{x}_k,\{\bm{u}_i\}_{i=k}^{N-1},k,N) = \Phi(\bm{x}_N,N) + \sum_{i=k}^{N-1} \mathcal{L}(\bm{x}_i,\bm{u}_i),
$$
for which we may define a *value function*
$$
V(\bm{x}_k,k,N) = \min_{\{\bm{u}_i\}_{i=k}^{N-1}} J(\bm{x}_k,\{\bm{u}_i\}_{i=k}^{N-1},k,N),
$$
and an optimal control policy
$$
\{\bm{u}^*_i\}_{i=k}^{N-1} = \argmin_{\{\bm{u}_i\}_{i=k}^{N-1}} J(\bm{x}_k,\{\bm{u}_i\}_{i=k}^{N-1},k,N),
$$
the application of which results in the system following an optimal trajectory $\{\bm{x}^*_i\}_{i=k}^N$.

The so-called *Bellman equation* can then be derived by formulating the value function for step $k$ recursively (using the value function for step $k+1$) as
$$
V(\bm{x}_k,k,N) = \min_{\bm{u}_k} \left(\mathcal{L}(\bm{x}_k,\bm{u}_k) + V(\bm{x}_{k+1},k+1,N)\right)
$$
and substituting $\bm{x}_{k+1}$ using the system's dynamics to attain the final form
$$
V(\bm{x}_k,k,N) = \min_{\bm{u}_k} \left(\mathcal{L}(\bm{x}_k,\bm{u}_k) + V(\bm{f}(\bm{x}_k,\bm{u}_k),k+1,N)\right).
$$


