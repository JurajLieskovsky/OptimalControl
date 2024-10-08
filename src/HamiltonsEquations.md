# Hamilton's Equations

Let us consider the problem
$$
\min_{y(x)\in\mathcal{C}^1} \int_a^b L(x,y(x),y^\prime(x))\, \mathrm{d}x, \quad y(a) = y_a, \quad y(b) = y_b.
$$
It's *First-Order Necessary Conditions (FONC)* come in the form of the *Euler-Lagrange* equation[^1]
$$
L_y(x,y,y^\prime) - (L_{y^\prime}(x,y,y^\prime))^\prime = 0. \tag{1}
$$

Let us define a variable $p(x)$ such that
$$
p = L_{y^\prime}(x,y,y^\prime).
$$
Requiring the satisfaction of the problem's FONC (eqn. 1) we may also define its derivative as
$$
p^\prime = L_y(x,y,y^\prime). \tag{2}
$$
Finally, let us also define the Hamiltonian (function)
$$
H(x,y,y^\prime) = py^\prime - L(x,y,y^\prime).
$$

## Extremization with respect to $y^\prime$
When extremized with respect to $y^\prime$, the Hamiltonian is necessarily maximized as
$$
H_{y^\prime}(x,y,y^\prime) = p - L_{y^\prime}(x,y,y^\prime) = 0
$$
and therefore the FONC is automatically satisfied. The second order necessary condition (SONC) then comes in the form
$$
L_{y^\prime y^\prime}(x,y,y^\prime) \geq 0
$$
as
$$
H_{y^\prime y^\prime}(x,y,y^\prime) = -L_{y^\prime y^\prime}(x,y,y^\prime).
$$


## Extremization with respect to $y$ and $p$
Extremization with respect to $y$ and $p$ then yields a set of FONC which can be, after substituting eqn. 2, manipulated into Hamilton's canonical equations
$$
\begin{aligned}
-p^\prime &= H_y(x,y,y^\prime) \\
y^\prime &= H_p(x,y,y^\prime).
\end{aligned}
$$
which can be viewed as equations governing the dynamics of a system with states $y$ and $p$.

---

[^1]: from this point on all variables that are functions of only $x$, such as $y(x)$, are written without $(x)$ in all display mode equations.
