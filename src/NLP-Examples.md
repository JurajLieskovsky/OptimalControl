# NLP Problem Examples

## Proportions of a canister
We are tasked with designing the proportions of a 0.5 liter cylindrical canister to minimize its surface area and therefore the amount of material used.

Cylinder's volume and surface are
$$
\begin{aligned}
	V &= \pi r^2 h \\
	S &= 2 \pi (r^2 + rh) \,.
\end{aligned}
$$

### Mathematical model
$$
\begin{aligned}
	\min_{r,h} & \quad 2 \pi (r^2 + rh) \\
	\text{s.t.} & \quad \pi r^2 h = 0.5\\
							& \quad r \geq 0 \\
							& \quad h \geq 0 
\end{aligned}
$$

As we are dealing with a quadratic objective function and a cubic equality constraint, the python package CVXPY does not have an interface to a suitable solver. Fortunately, the julia package JuMP does.
