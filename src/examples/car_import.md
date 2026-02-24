# Car Importer
A car importer is planning to import two models of JDM cars. In one shipment he can transport 60 cars at an investment of 50 million CZK. The purchase price of the two models is 2.5 million and 0.5 million CZK. He then expects a profit of 250 thousand CZK per unit sold of the first model and 75 thousand CZK of the second model. How many units of each model should he buy to maximize his profit, expecting every car will be sold?

## Mathematical Model
$$
\begin{aligned}
	\max_{x_1, x_2} & \quad 0.25 x_1 + 0.075 x_2 \\
	\text{s.t.} & \quad x_1 \geq 0 \\
							& \quad x_2 \geq 0 \\
							& \quad x_1 + x_2 \leq 60 \\
							& \quad 2.5 x_1 + 0.5 x_2 \leq 50
\end{aligned}
$$

### Canonical form
$$
\begin{aligned}
	\max_{x} & \quad c^\top x \\
	\text{s.t.} & \quad x \geq 0 \\
							& \quad A x \leq b \\
\end{aligned}
$$
where
$$
\begin{aligned}
c &= \begin{bmatrix} 0.25 \\ 0.075 \end{bmatrix} \\
A &= \begin{bmatrix} 1 & 1 \\ 2.5 & 0.5 \end{bmatrix} \\
b &= \begin{bmatrix} 60 \\ 50 \end{bmatrix}
\end{aligned}
$$

