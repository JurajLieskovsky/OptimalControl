# LP Problem Examples

## Car importer
A car importer is planning to import two models of JDM cars. In one shipment he can transport 60 cars and investment of 50 million CZK. The purchase price of the two models is 2.5 million and 0.5 million CZK. He then expects a profit of 250 thousand CZK per unit sold of the first model and 75 thousand CZK of the second model. How many units of each model should he buy to maximize his profit, expecting every car will be sold?

### Mathematical model
$$
\begin{aligned}
	\max_{x_1, x_2} & \quad 0.25 x_1 + 0.075 x_2 \\
	\text{s.t.} & \quad x_1 \geq 0 \;,\, x_2 \geq 0 \\
							& \quad x_1 + x_2 \leq 60 \\
							& \quad 2.5 x_1 + 0.5 x_2 \leq 50
\end{aligned}
$$

### Code
- [julia - JuMP](https://github.com/lieskjur/nmoc-julia/blob/main/src/car_import.jl)
- [python - CVXPY](https://github.com/lieskjur/nmoc-python/blob/main/src/car_import.py)

## Flow optimization
We have a network (represented as directed graph). The graph has a "Source" of a medium (it can be for example gas, water or electricity) and Sink with additional nodes in between. All edges between source and sink has defined maximal capacity.

```mermaid
graph LR;
    A["Source"];
		D["Sink"];
		A-->|"10"|B1;
    A-->|"8"|B2;
    A-->|"5"|C1;
    B1-->|"6"|C1;
		B1-->|"2"|C2;
		B2-->|"4"|C1;
		B2-->|"5"|C2;
		C1-->|"8"|D;
		C2-->|"9"|D;
```
What is the maximum amount medium we can transmit through the sink?

### Mathematical model

Let us first define our optimization variables $x_i$ as individual flows through the edges of our graph

```mermaid
graph LR;
    A["Source"];
		D["Sink"];
		A-->|"x₂ ≤ 10"|B1;
    A-->|"x₃ ≤ 8"|B2;
    A-->|"x₁ ≤ 5"|C1;
    B1-->|"x₄ ≤ 6"|C1;
		B1-->|"x₅ ≤ 2"|C2;
		B2-->|"x₆ ≤ 4"|C1;
		B2-->|"x₇ ≤ 5"|C2;
		C1-->|"x₈ ≤ 8"|D;
		C2-->|"x₉ ≤ 9"|D;
```

we may then write the problem as

$$
\begin{aligned}
	\max_{\bm{x}} & \quad x_8 + x_9 \\
	\text{s.t.} & \quad \bm{0} \leq \bm{x} \leq \bm{u} \\
							& \quad x_4 + x_5 = x_2 \\
	            & \quad x_6 + x_7 = x_3 \\
	            & \quad x_8 = x_5 + x_6 + x_4 \\
	            & \quad x_9 = x_5 + x_7 \\
\end{aligned}
$$
where
$$
\bm{u}^\top = \begin{bmatrix} 5 & 10 & 8 & 6 & 2 & 4 & 5 & 8 & 9 \end{bmatrix}
$$

### Canonical form
Manipulating the objective into the canonical form can be done simply with
$$
\bm{c}^\top = \begin{bmatrix}
	0 & 0 & 0 & 0 & 0 & 0 & 0 & 1 & 1 \\
\end{bmatrix}
\,.
$$
To deal with the constraints let us first formulate the equality constraints in matrix form as:
$$
\bm{A}_{\mathrm{eq}} \bm{x} = \bm{0}
$$
where
$$
\bm{A}_{\mathrm{eq}} =
\begin{bmatrix}
	0 & -1 & 0 & 1 & 1 & 0 & 0 & 0 & 0 \\
	0 & 0 & -1 & 0 & 0 & 1 & 1 & 0 & 0 \\
	0 & 0 & 0 & -1 & -1 & -1 & 0 & 1 & 0 \\
	0 & 0 & 0 & 0 & -1 & 0 & -1 & 0 & 1 \\
\end{bmatrix}
\,.
$$
Equivalently we may write it as
$$
\bm{0} \leq \bm{A}_{\mathrm{eq}} \bm{x} \leq \bm{0} \,.
$$
Together with the upper bounds they can be now rewritten into the canonical form
$$
\underbrace{
\begin{bmatrix}
	\bm{E} \\
	\bm{A}_{\mathrm{eq}} \\
	-\bm{A}_{\mathrm{eq}}
\end{bmatrix}
}_{\bm{A}}
\bm{x}
\leq
\underbrace{
\begin{bmatrix}
	\bm{u} \\
	\bm{0} \\
	\bm{0}
\end{bmatrix}
}_{\bm{b}}
$$
