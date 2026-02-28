# Economic Dispatch
We have three power plants each producing electricity to satisfy the demand of $s = 3000$. Each of the power plants has an upper and lower capacity limit $u_i$ and $l_i$ and a quadratic model of the cost associated with its power output $a_i + b_i P_i + c_i P_i^2$. Numerical values for the capacity limits and cost coefficients are provided in the table bellow.

| $i$         | $a_i$ | $b_i$ | $c_i$ | $l_i$ | $u_i$ |
|-------------|-------|-------|-------|-------|-------|
| 1           | 20    | 5     | 0.02  | 200   | 1000  |
| 2           | 25    | 4     | 0.015 | 300   | 1500  |
| 3           | 30    | 3     | 0.01  | 100   | 800   |

How much power should each power plant provide, to minimize the overall cost?

## Mathematical Model
### Always ON

Assuming all power plants must be powered on at all times, the problem can be modeled as

$$
\begin{aligned}
	\min_{x_{1:3}} & \quad \sum_{i=1}^{3} a_i + b_i x_i + c_i x_i^2 \\
	\text{s.t.} & \quad l_i \leq x_i \leq u_i \,,\quad \forall i \in \{1, \ldots, 3\} \\
							& \quad \sum_{i=1}^{3} x_i = s \\
\end{aligned}
$$

### ON/OFF

Lets now assume that we may also power on/off each power plant based on the demand. This necessitates the inclusion of additional binary decision variables $z_i$ in the problem

$$
\begin{aligned}
	\min_{x_{1:3}, z_{1:3}} & \quad \sum_{i=1}^{3} z_i a_i + b_i x_i + c_i x_i^2 \\
	\text{s.t.} & \quad z_i \, l_i \leq x_i \leq z_i \, u_i \,,\quad \forall i \in \{1, \ldots, 3\} \\
							& \quad \sum_{i=1}^{3} x_i = s \\
							& \quad z_i \in \{0,1\}.
\end{aligned}
$$

The problem remains quadratic but, due to the binary decision variables $z_i$, is now classified as a MIQP.
