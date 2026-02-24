# Maximum Flow Optimization
We have a network (represented as directed graph). The graph has a "Source" of a medium (it can be for example gas, water, or electricity) and Sink with additional nodes in between. All edges between source and sink has defined maximal capacity.

```mermaid
graph LR;
    A["Source"];
		D["Sink"];
		A-->|"10"|B1;
    A-->|"8"|B2;
    B1-->|"6"|C1;
		B1-->|"2"|C2;
		B2-->|"4"|C1;
		B2-->|"5"|C2;
		C1-->|"8"|D;
		C2-->|"9"|D;
```
What is the maximum amount medium we can transmit through the sink?

## Mathematical Model

Let us first define our optimization variables $x_i$ as individual flows through the edges of our graph

```mermaid
graph LR;
    A["Source"];
		D["Sink"];
		A--->|"x₀ ≤ 10"|B1;
    A--->|"x₁ ≤ 8"|B2;
    B1-->|"x₂ ≤ 6"|C1;
		B1-->|"x₃ ≤ 2"|C2;
		B2-->|"x₄ ≤ 4"|C1;
		B2-->|"x₅ ≤ 5"|C2;
		C1-->|"x₆ ≤ 8"|D;
		C2-->|"x₇ ≤ 9"|D;
```

we may then write the problem as

$$
\begin{aligned}
	\max_{x} & \quad x_6 + x_7 \\
	\text{s.t.} & \quad 0 \leq x \leq u \\
							& \quad x_0 = x_2 + x_3 \\
	            & \quad x_1 = x_4 + x_5 \\
	            & \quad x_2 + x_4 = x_6 \\
	            & \quad x_3 + x_5 = x_7 \\
\end{aligned}
$$
where
$$
u^\top = \begin{bmatrix} 10 & 8 & 6 & 2 & 4 & 5 & 8 & 9 \end{bmatrix}
$$

### Canonical Form
Manipulating the objective into the canonical form can be done simply with
$$
c^\top = \begin{bmatrix}
	 0 & 0 & 0 & 0 & 0 & 0 & 1 & 1 \\
\end{bmatrix}
\,.
$$
To deal with the constraints let us first formulate the equality constraints in matrix form as:
$$
A_{\mathrm{eq}} x = 0
$$
where
$$
A_{\mathrm{eq}} =
\begin{bmatrix}
	-1 & 0 & 1 & 1 & 0 & 0 & 0 & 0 \\
	0 & -1 & 0 & 0 & 1 & 1 & 0 & 0 \\
	0 & 0 & -1 & 0 & -1 & 0 & 1 & 0 \\
	0 & 0 & 0 & -1 & 0 & -1 & 0 & 1 \\
\end{bmatrix}
\,.
$$
Equivalently we may write it as
$$
0 \leq A_{\mathrm{eq}} x \leq 0 \,.
$$
Together with the upper bounds they can be now rewritten into the canonical form
$$
\underbrace{
\begin{bmatrix}
	I \\
	A_{\mathrm{eq}} \\
	-A_{\mathrm{eq}}
\end{bmatrix}
}_{A}
x
\leq
\underbrace{
\begin{bmatrix}
	u \\
	0 \\
	0
\end{bmatrix}
}_{b}
$$

