# Linear-Quadratic MPC

Model predictive control (MPC) is a control strategy which relies on the system's model to predict and optimize its trajectory online, applying inputs from the beginning of the predicted horizon. There are many algorithms for trajectory optimization, each adapted for a specific use-case. When talking about nonlinear systems in general, main factors determining the applicability of a specific algorithm are if the system is represented in continuous or discrete time and if its dynamics are continuous or hybrid.

<!--
Considerations when choosing between suitable algorithms include the option to supply an initial guess of the optimal trajectory (even if infeasible), strictly feasible iterates of the predicted trajectory, 
-->

In this course we will limit ourselves to the specific case of linear systems represented in discrete time with a quadratic objective (LQ control problem) and box constraints on the system's inputs[^1]. In contrast to the LQR where the problem is solved on an infinite horizon we will be solving the optimal control problem on a finite horizon which is almost universally the case in MPC.

This specific control problem can be transcribed into a QP problem with specialized solvers dedicated to finding its solution. We will go through two formulations of this problem:
* direct - both states $x_k$ and inputs $u_k$ are the decision variables,
* indirect - only inputs $u_k$ are decision variables.

---

[^1]: could be extended to linear inequality constraints on both inputs and states
