# Linear-Quadratic Regulator

The linear-quadratic regulator gets its name from the linear model of the system and the quadratic cost function used for its design. For these, the optimal controller can be derived analytically and takes the form of linear state feedback making its implementation particularly simple.

The systems can be described in both the discrete-time and continuous-time domain and particular variants of the LQR allow for time-variant systems. Cost functions must then reflect the type of the system. For time-invariant systems, the cost function can either take the form of a time-invariant running cost integrated over an infinite horizon, or a sum of a final cost and a running cost (optionally time-variant) integrated over a finite horizon. If the system is time-variant, only the second option is available.

In the following sections we will cover four variants based on the time-domain and horizon
- discrete-time x continuous-time,
- finite-horizon x infinite-horizon.

Many more variants exist including those for reference tracking, dead-beat control, and even nonlinear trajectory optimization.
