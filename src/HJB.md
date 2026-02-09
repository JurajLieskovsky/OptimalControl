# Hamilton-Jacobi-Bellman Equation
Let us assume we are trying to minimize the total cost
$$
J(x(t_0),u(\tau),t_0) = \Phi(x(t_f)) + \int_{t_0}^{t_f} l(x(\tau),u(\tau),\tau) \, d\tau .
$$
of a continuous-time system's trajectory $x(\tau)$, $\tau \in [t_0, t_f]$ with dynamics in the form
$$
\dot{x}(t) = f(x(t),u(t),t) ,
$$
starting from the state $x(t_0) = \tilde{x}_0$.


The concept of the total cost can be generalized for any $t \in [t_0, t_f]$ to a cost-to-go
$$
J(x(t),u(\tau),t) = \Phi(x(t_f)) + \int_{t}^{t_f} l(x(\tau),u(\tau),\tau) \, d\tau ,
$$
for which we may define a value function
$$
\begin{aligned}
V(x(t),t) = \min_{u(\tau)} &\enspace J(x(t),u(\tau),t), \quad \tau \in [t, t_f) , \\
\text{s.t.} &\enspace \dot{x}(\tau) = f(x(\tau),u(\tau),\tau), \quad \forall \tau \in [t, t_f] 
\end{aligned}
$$
and optimal control policy
$$
\begin{aligned}
u^*(\tau) = \argmin_{u(\tau)} &\enspace J(x(t),u(\tau),t), \quad \tau \in [t, t_f) , \\
\text{s.t.} &\enspace \dot{x}(\tau) = f(x(\tau),u(\tau),\tau), \quad \forall \tau \in [t, t_f] 
\end{aligned}
$$
the application of which results in the system following an optimal trajectory $x^*(\tau)$, $\tau \in (t,t_f]$.

For the previously defined value function the Hamilton-Jacobi-Bellman (HJB) equation can be derived[^2] as
$$
-\frac{\partial V}{\partial t}(x(t),t) = \min_{u(t)} \left(l(x(t),u(t),t) + \left(\frac{\partial V}{\partial x}\right)^\top\!(x(t),t) \, f(x(t),u(t),t) \right) .
$$

---

[^2]: An overview of the derivation is presented by Steven Brunton in one of his videos @@Brunton2022-HJB also available [here](https://www.youtube.com/watch?v=-hO-AnFYm6M&ab_channel=SteveBrunton). As a note, there is a small mistake, acknowledged by the presenter in the comments, at [9:11](https://www.youtube.com/watch?v=-hO-AnFYm6M&t=551s) of the video where "$0$" should be replaced with "$t$".

<!--
### HBJ Derivation
$$
\frac{d}{dt} V(x(t),t,t_f) = \min_{u(t)} \frac{d}{dt} J(x(t),u(t),t,t_f) 
$$
$$
  \frac{d}{dt} V(x(t),t,t_f) = \frac{\partial V}{\partial t} + \left(\frac{\partial V}{\partial x}\right)^\top \frac{d{x}^*}{dt}
$$
$$
\begin{aligned}
\min_{u(t)} \frac{d}{dt} J(x(t),u(t),t,t_f) &= \min_{u(t)} \frac{d}{dt} \left(\Phi(x(t_f)) + \int_{t}^{t_f} l(x(\tau),u(\tau)) \, d\tau \right) \\
&= \min_{u(t)} \left( \frac{d}{dt} \int_{t}^{t_f} l(x(\tau),u(\tau)) \, d\tau \right) \\
&= \min_{u(t)} -l(x(t),u(t)) 
\end{aligned}
$$
--->
