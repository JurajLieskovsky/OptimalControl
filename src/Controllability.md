# Controllability/Reachability

Controllability and reachability are defined for discrete-time systems as:

- A system is controllable if from any state $x_0 \in \Reals^n$ one can achieve the state $x_N = 0$ using a series of inputs $u_{0:N-1}$.
- A state $x_N \in \Reals^n$ is reachable if it can be achieved by applying a series of inputs $u_{0:N-1}$ when starting from the initial state $x_0 = 0$.

For continuous-time systems they are similarly defined as:

- A system is controllable if from any state $x(0) \in \Reals^n$ one can achieve the state $x(t) = 0$ using a control policy $u(\tau)$, $\tau \in \langle 0, t)$.
- A state $x(t) \in \Reals^n$ is reachable if it can be achieved by applying a control policy $u(\tau)$, $\tau \in \langle 0, t)$ when starting from the initial state $x(0) = 0$.

For linear systems all states are reachable if the system is controllable.
