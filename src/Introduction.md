These are notes for tutorials of the subject "Optimal and Predictive Control System" taught at the Faculty of Mechanical Engineering at the Czech Technical University in Prague.

Dating back to the 1950s optimal control is an every evolving field currently fueled by the incredible amounts of computational power at our disposal. Although in this course we only cover the fundamentals as applied to linear system which can be successfully implemented on microcontrollers, cutting-edge approaches push hardware to its limits, allowing for the control of walking robots, autonomous vehicles, etc.

The materials are loosely divided into three blocks. We cover the basics of numerical optimization which we will become relevant for optimal control only at the very end of the course. Regardless we will attempt to provide examples that demonstrate their utility as we go. Then we will move on to the main content of the course. Starting from the quite abstract concept of the Bellman principle we cover the topic of the linear-quadratic regulator (LQR) from which we will transition to model predictive control (MPC).

We will apply each control strategy to the system of a bi-rotor, i.e. a quad-rotor simplified into the horizontal plane. As supplementary materials we will show how its dynamic model can be derived.

DISCLAIMER: These notes have not gone through a peer review process and are likely to contain (hopefully only minor) mistakes.
