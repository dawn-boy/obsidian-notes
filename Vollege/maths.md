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
a linear PDE is of the form Pp + Qq = R, where P, Q, R are functions of x, y, z is known as legrange's linear PDE.

consider, a subsidiary equations,
$$ \frac{dx}{P} = \frac{dy}{Q} = \frac{dz}{R}$$
take any 2 combination from the subsidiary equation, eg: 
$$ \frac{dx}{P} = \frac{dy}{Q}, or, \frac{dy}{Q}=\frac{dz}{R},or, \frac{dx}{P}=\frac{dz}{R}$$
- move all the X terms to dx side, and Y terms to dy side. Integrating a combination we get, 
$$ u(x,y) \implies \int \frac{dx}{P} = \int\frac{dy}{Q}\implies C_1$$

- move all the Y terms to dy side, and Z terms to dz side. Integrating another combination, we get 
$$v(y,z) =\int\frac{dy}{Q} = \int\frac{dz}{R} \implies C_2$$

- now combine both the answer likewise,

$$\phi(u,v) \implies \phi(C_1,C_2) = 0 $$
#### Note
If you cannot move the particular variable to it's differentiation side, or if there's a third variable that do not belong anywhere, then differentiation here is not possible. Choose another combination from your lovely subsidiary equation.

## 2nd Method
Consider a subsidiary equation,
$$ \frac{dx}{P} = \frac{dy}{Q} = \frac{dz}{R}$$
- Choose the multipliers l, m, n, such that
$$ lP+mQ+nR = 0$$
- if, 
$$ \frac{ldx}{lP} = \frac{mdy}{mQ} =\frac{ndz}{nR} $$
$$\frac{ldx+mdy+ndz}{lP+mQ+nR}=\frac{ldx+mdy+ndz}{0}=0 $$
- then,
$$ u(x,y) = \int l_1dx+ \int m_1dy+\int n_1dz = C_1$$
- and,
$$ v(y,z) = \int l_2dx+ \int m_2dy+\int n_2dz = C_2$$
- so,
$$ \phi(u,v) = \phi(C_1,C_2) = 0$$
---
The general form of homogeneous PDE is
$$ A_n\frac{\partial^nz}{\partial x^n}+A_{n-1}\frac{\partial^nz}{\partial x^{n-1} 
\partial y }+ ...+A_{i}\frac{\partial^nz}{\partial y_n } = f(x,y)$$
where, A<sub>n</sub>, A<sub>n-1</sub>, A<sub>i</sub> are constants.
The differential operators are,
$$D = \frac{\partial}{\partial x},$$
$$D' = \frac{\partial}{\partial y}$$
So the Solution of a homogeneous PDE is,
$$z = Complementary Function + PartialIntegral$$
- To find the C.F,
- take the LHS of PDE and substitute,
$$D =m, D'=1$$
- we get an auxiliary equation. Just solve for m<sub>1</sub> and m<sub>2</sub> values.
- case 1: roots are different,
$$C.F = \phi_1(y+m_1x)+\phi_2(y+m_2x)$$
- case 2: roots are equal,
$$C.F= \phi_1(y+m_1x)+x\phi_2(y+m_1x)$$
