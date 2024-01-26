# partial differential equation
- PDE is a mathematical equation that involves two or more independent variables
- the order of PDE is the highest derivative
- the degree of the PDE is the power of the highest derivative term
## solve the equation for z
$$\frac{\partial^2{z}}{\partial{x^2}} + 7 = 0$$on integrating w.r.t x,
(cuz x is in the denominator and that's considered as integration)
$$\frac{\partial{z}}{\partial{x}} + 7x = f(y)$$
integrating again,
$$ z + \frac{7x^2}{2} = g(y) + xf(y)$$
so value of z is,
$$ z = -\frac{7x^2}{2} + g(y) + xf(y) $$

- a linear PDE is of the form Pp + Qq = R where P, Q, R are the functions of x, y, z which is known as the le grange's linear PDE.

***
## Linear PDE
- a linear PDE is of the form Pp + Qq = R, where P, Q, R are functions of x, y, z is known as legrange's linear PDE.
- consider, a subsidiary equations,
- $$ \frac{dx}{P} = \frac{dy}{Q} = \frac{dz}{R}$$
- take any 2 combination from the subsidiary equation, 
- Case 1: Integrating, we get u(x,y) = C<sub>1</sub>
- Case 2: Integrating, we get v(y,z) = C<sub>2</sub>
- Case 3: $\phi$(u,v) = $\phi$(C<sub>1</sub>,C<sub>2</sub>) = 0 