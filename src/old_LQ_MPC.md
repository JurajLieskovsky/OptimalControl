# Linear-Quadratic MPC

Model predictive control (MPC) is a control strategy which relies on the system's model to predict and optimize its trajectory online, periodically re-optimizing the trajectory as a form of feedback. If a linear representation of the system and a quadratic running and final cost are used, it is essentially an extension of the finite-horizon LQR that includes control in state inputs. This is in fact what is commonly referred to as MPC. If the system's dynamics are nonlinear or the cost functions contain terms that are not linear nor quadratic, the strategy is referred to as nonlinear MPC. 

In this course we will limit ourselves only to the former case which can be transcribed into a QP problem. We will go through two formulations of this problem based on how the system's dynamics are incorporated into the optimization problem:
* explicitly constrained - both states $\bm{x}_k$ and inputs $\bm{u}_k$ are the decision variables,
* implicitly constrained - only inputs $\bm{u}_k$ are decision variables.
