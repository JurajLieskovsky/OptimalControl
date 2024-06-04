# Linear-Quadratic MPC

Model predictive control (MPC) is a control strategy which relies on the system's model to predict and optimize its trajectory online, applying inputs from the beginning of the predicted horizon. There are many algorithms for trajectory optimization, each adapted for a specific use-case. When talking about nonlinear systems in general, main factors determining the applicability of a specific algorithm are if the system is represented in continuous or discrete time and if its dynamics are continuous or hybrid.

<!--
Considerations when choosing between suitable algorithms include the option to supply an initial guess of the optimal trajectory (even if infeasible), strictly feasible iterates of the predicted trajectory, 
-->

In this course we will limit ourselves to the specific case of linear systems[^1] represented in discrete time with a quadratic objective (LQ control problem) and box constraints on the system's inputs [^2]. This specific control problem can be transcribed into a QP problem with specialized solvers dedicated to finding its solution. We will go through two formulations of this problem:
* direct - both states $\bm{x}_k$ and inputs $\bm{u}_k$ are the decision variables,
* indirect - only inputs $\bm{u}_k$ are decision variables.

---

[^1]: With some slight modification it can also be applied to the control of nonlinear system's near a fixed point.

[^2]: There are no obstacles preventing us from also adding linear inequality constraints to states.
