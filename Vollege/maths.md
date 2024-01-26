# module 1
## partial differential equation
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
#### ==Note
If you cannot move the particular variable to it's differentiation side, or if there's a third variable that do not belong anywhere, then differentiation here is not possible. Choose another combination from your lovely subsidiary equation.==
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
## homogeneous PDE
The general form of homogeneous PDE is
$$ A_n\frac{\partial^nz}{\partial x^n}+A_{n-1}\frac{\partial^nz}{\partial x^{n-1} 
\partial y }+ ...+A_{i}\frac{\partial^nz}{\partial y_n } = f(x,y)$$
where, A<sub>n</sub>, A<sub>n-1</sub>, A<sub>i</sub> are constants.
The differential operators are,
$$D = \frac{\partial}{\partial x},$$
$$D' = \frac{\partial}{\partial y}$$
So the Solution of a homogeneous PDE is,
$$z = Complementary Function + PartialIntegral$$
### complementary function
equate the LHS of the PDE to zero and substitute,
$$D =m, D'=1$$
we get an auxiliary equation. Just solve for m<sub>1</sub> and m<sub>2</sub> values.
- type 1: roots are different,
$$C.F = \phi_1(y+m_1x)+\phi_2(y+m_2x)$$
- type 2: roots are equal,
$$C.F= \phi_1(y+m_1x)+x\phi_2(y+m_1x)$$
### partial integral
$$ P.I = \frac{1}{f(D,D')} * f(x,y) $$
- type 1: $f(x,y) = e^{ax+by}$, 
$$D=a, $$
$$D' = b$$
- type 2: $f(x,y) = sin(ax+by)$ or $cos(ax+by)$
$$D^2 = -a^2,$$
$$DD' = -ab$$
$$D'^2 = -b^2$$
	- to substitute the D<sup>2</sup>, DD', D'<sup>2</sup> values, there should be an exact match, i.e we cannot substitute a value for D based on D<sup>2</sup>. So, in that case, just rationalize the denominator to get a D<sup>2</sup>.

- type 3: $f(x,y)  = x^my^n$ 
	- take the highest derivative of D outside and make the whole equation of the form $(1\pm x)$ 
	- take the term to the numerator, $(1 \pm x)^{-1}$, and apply the **Binomial Expansion Formulas**.
		- $(1+x)^{-1} = (1-x+x^2-x^3+...)$
		- $(1-x)^{-1} = (1+x+x^2+x^3+...)$ 
	- if the f(x,y) differentiates to 0 at the x<sup>nth</sup> term, then no need to write anymore x terms after that.

- type 4: f(x,y) = 0, then there is no P.I to the PDE.

==note:==
- $\frac{1}{D}$ means integrating with respect to x, and
- $\frac{1}{D'}$ means integrating with respect to y.
#### binomial theorem
let there be an equation!
$$ ax + by -c = 0 $$
then,
$$ \frac{-b \pm \sqrt{b^2-4ac}}{2a} $$
## solution to PDE of some standard forms
the solution of a PDE is a relation between it's independent and dependent variables.

- complete solution
	if, number of independent variables = number of arbitrary constants.

- singular solution
	differentiate the complete solution with respect to a,b and eliminate a,b. 

- particular solution
	in complete solution, give a particular value to the arbitrary constant.

- general solution
	in complete solution, take b = f(a) and eliminate a.

### types
1) f(p,q) = 0
	then let z = ax + by + c, be the solution.
	
	differentiate z w.r.t x,
$$\frac{\partial z}{\partial x} = a \implies p = a$$
	differentiate z w.r.t y,
$$\frac{\partial z}{\partial y} = b \implies q = b$$
	substitute p and q values in the equation and equate it to b. Then, substitute the b value in z.
	Finally, find the C.S, S.S, P.S, and G.S.

2) f(p,q,z) = 0
	then let z = f(u), where u = x + ay be the solution.

	differentiate z w.r.t x,
	$$\frac{\partial z}{\partial x} = \frac{\partial z}{\partial u} * \frac{\partial u}{\partial x}$$
	since u = x + ay and $\frac{\partial u}{\partial x} = 1$
$$ \frac{\partial z}{\partial x} = \frac{\partial z}{\partial u} * 1 \implies p = \frac{\partial z}{\partial u}$$
	differentiate z w.r.t y,
	$$\frac{\partial z}{\partial y} = \frac{\partial z}{\partial u} * \frac{\partial u}{\partial y}$$
	since u = x + ay and $\frac{\partial u}{\partial y} = a$
$$ \frac{\partial z}{\partial y} = \frac{\partial z}{\partial u} * a \implies p = \frac{a\partial z}{\partial u}$$
	substitute p and q values in the equation and move the $\partial u$ terms to one side and $\partial x$ or $\partial y$ term to the other side. Now, integrate on both sides. Move z to L.H.S and all other terms to R.H.S.
	finally, find the C.S, S.S, P.S, G.S.

3) f(p,q,x,y) = 0
	An equation containing p,q,x,y and if it is possible to separate x,p and y,q, such equation is called separable.
	
	then let $z = \int{pdx}+\int{qdy}$, 

	separate p,x terms to one side and q,y terms to the other side, and equate them all to a.
	eg:
		$p+q = x+y$
		$p-x = y-q = a$
		$p-x = a \implies p = a+x$
		$y-q=a \implies q=y-a$
	Now, substitute the p,q values in z, and integrate them.
	finally, find the C.S, S.S, P.S, G.S.
4) clairant's form
	then let z = ax + by + f(a,b)

	differentiating z w.r.t x,
$$\frac{\partial z}{\partial x} = a \implies p = a$$
	differentiating z w.r.t y,
$$\frac{\partial z}{\partial y} = b \implies q = b$$
	now, substitute the p,q values in z
	finally, find the C.S, S.S, P.S, G.S.
***
# module 2
