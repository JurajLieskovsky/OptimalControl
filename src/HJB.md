# Hamilton-Jacobi-Bellman Equation
Let us assume we are trying to minimize the total cost
$$
J(\bm{x}(t_0),\bm{u}(\tau),t_0,t_f) = \Phi(\bm{x}(t_f),t_f) + \int_{t_0}^{t_f} \mathcal{L}(\bm{x}(\tau),\bm{u}(\tau)) \, d\tau .
$$
of a continuous-time system's trajectory $\bm{x}(\tau)$, $\tau \in \langle t_0, t_f \rangle$ with dynamics in the form
$$
\frac{d\bm{x}}{d\tau}(\tau) = \bm{f}(\bm{x}(\tau),\bm{u}(\tau)) ,
$$
starting from the state $\bm{x}(t_0) = \tilde{\bm{x}}_0$.


The concept of the total cost can be generalized for any $t \in \langle t_0, t_f \rangle$ to a *cost-to-go*
$$
J(\bm{x}(t),\bm{u}(\tau),t,t_f) = \Phi(\bm{x}(t_f),t_f) + \int_{t}^{t_f} \mathcal{L}(\bm{x}(\tau),\bm{u}(\tau)) \, d\tau ,
$$
for which we may define a *value function*
$$
V(\bm{x}(t),t,t_f) = \min_{\bm{u}(\tau)} J(\bm{x}(t),\bm{u}(\tau),t,t_f),
$$
and optimal control policy
$$
\bm{u}^*(\tau) = \argmin_{\bm{u}(\tau)} J(\bm{x}(t),\bm{u}(\tau),t,t_f), \quad \tau \in \langle t, t_f )
$$
the application of which results in the system following an optimal trajectory $\bm{x}^*(\tau)$, $\tau \in (t,t_f\rangle$.

For the previously defined value function the *Hamilton-Jacobi-Bellman (HJB) equation* can be derived[^2] as
$$
-\frac{\partial V}{\partial t} = \min_{\bm{u}(t)} \left(\mathcal{L}(\bm{x}(t),\bm{u}(t)) + \left(\frac{\partial V}{\partial x}\right)^\top \bm{f}(\bm{x}(t),\bm{u}(t)) \right) .
$$

---

[^2]: An overview of the derivation is presented by Steven Brunton in one of his videos @@Brunton2022-HJB also available [here](https://www.youtube.com/watch?v=-hO-AnFYm6M&ab_channel=SteveBrunton). As a note, there is a small mistake, acknowledged by the presenter in the comments, at [9:11](https://www.youtube.com/watch?v=-hO-AnFYm6M&t=551s) of the video where "$0$" should be replaced with "$t$".

<!--
### HBJ Derivation
$$
\frac{d}{dt} V(\bm{x}(t),t,t_f) = \min_{\bm{u}(t)} \frac{d}{dt} J(\bm{x}(t),\bm{u}(t),t,t_f) 
$$
$$
  \frac{d}{dt} V(\bm{x}(t),t,t_f) = \frac{\partial V}{\partial t} + \left(\frac{\partial V}{\partial x}\right)^\top \frac{d{\bm{x}}^*}{dt}
$$
$$
\begin{aligned}
\min_{\bm{u}(t)} \frac{d}{dt} J(\bm{x}(t),\bm{u}(t),t,t_f) &= \min_{\bm{u}(t)} \frac{d}{dt} \left(\Phi(\bm{x}(t_f),t_f) + \int_{t}^{t_f} \mathcal{L}(\bm{x}(\tau),\bm{u}(\tau)) \, d\tau \right) \\
&= \min_{\bm{u}(t)} \left( \frac{d}{dt} \int_{t}^{t_f} \mathcal{L}(\bm{x}(\tau),\bm{u}(\tau)) \, d\tau \right) \\
&= \min_{\bm{u}(t)} -\mathcal{L}(\bm{x}(t),\bm{u}(t)) 
\end{aligned}
$$
--->
