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
 ## vectors
a quantity is said to be a vector if it posses two independent quality, i.e, magnitude and direction.

## group
a non-empty set S, with binary operation * in (S,\*) is said to be a group if the following property satisfy,
- closure property
$$\forall \ a,b \in S \implies a*b \in S$$
- associative property
$$\forall \ a,b,c \in S \implies a*(b*c) = (a*b)*c$$
- identity property
$$\forall \ a \in S\ , e \in S, such\ that,$$
$$a*e= a$$
- inverse property
$$\forall \ a \in S, a^{-1} \in S, such \ that,$$
$$a * a^{-1} = e$$
### abelian group
a set (S,\*) is said to be an abelian group if it satisfies all the properties that makes it a group and if it satisfies the below property
- commutative property
$$\forall \ a,b \in S \implies a*b = b*a$$
==Note:
The set can be anything like R(real), Z(integers), N(natural), etc.. and the operations can also be anything like +, \*, etc.
the properties must adapt to the given operator, 
eg: commutative property for (S,+) is a+b = b+a, while for (S,\*) is a\*b = b\*a.==

- closed cell 
	- closure property
- semigroup 
	- closure property,
	- associative property.
- monoid 
	- closure property,
	- associative property
	- identity property
- abelian 
	- closure property
	- associative property
	- identity property
	- inverse property
	- commutative property
## vector space
a non-empty subset V (V,+,\*) is called a real vector space, if V with two binary operations (+,\*) satisfies the following conditions,
- (V,+) is an abelian group
- $\alpha(u,v) = \alpha u+\alpha v$ 
- $(\alpha+\beta)u = \alpha u + \beta u$
- $(\alpha \beta)u = \alpha(\beta u) = \beta(\alpha u)$
- $1 * u = u$
then (V,+,\*) is a real vector space.

### subset of a vector space
let W be the subset of a vector space (V,+,\*), then W is said to be a subspace of V, if it satisfies the following,
- W is a non-empty subset of V,
- $\forall \ u,v \in W \implies u+v \in W$
- $\forall \ \alpha,\beta \in R,\forall \ u,v \in W,\ \implies \alpha u+\beta v \in W$

if W<sub>1</sub>, W<sub>2</sub> are subspaces of a vector space V, then W<sub>1</sub>$\ \cap$ W<sub>2</sub> is always a subspace of V.
if W<sub>1</sub>, W<sub>2</sub> are subspaces of a vector space V, then W<sub>1</sub>$\ \cup$ W<sub>2</sub> is a subspace of V, only if W<sub>1</sub> $\subseteq$ W<sub>2</sub> or W<sub>2</sub> $\subseteq$ W<sub>1</sub>

## linear combination
if $u_1,u_2,\ ... \ , u_n$ are the n vectors of the vector space V, then for any vector v $\in$ V, where $v=\alpha_1u_1+\alpha_2u_2+\ ... \ +\alpha_nu_n$ and $\alpha_1,\alpha_2,\ ... \ ,\alpha_n$ are scalars is called linear combination.

- if all $\alpha_i$ are 0, then the L.C is said to be a trivial L.C.
	**trivial L.C always gives zero vector.**
- if all $\alpha_i$ are not 0, then the L.C is said to be a non-trivial L.C
	**not-trivial L.C may or may not give zero vector.**

### for L.C
if the $\alpha_i$ values are
- 0     --> trivial, linearly independent
- not 0 --> non-trivial, linearly dependent
### for matrix determinant
if the determinant values are
- 0     --> non-trivial, linearly dependent
- not 0 --> trivial, linearly independent

#### to check if a set of vectors form linearly dependent or linearly independent
$$(1,0,1)\ (1,1,0) \ (1,-1,1) \ (1,2,-3)$$
$$\alpha_1(1,0,1) + \alpha_2(1,1,0) + \alpha_3(1,-1,1)+  \alpha_4(1,2,-3) = 0$$
- multiply all the scalars with the first element in the vector,
$$\alpha_1+\alpha_2+\alpha_3+\alpha_4 = 0$$
- now, multiply all the scalars with the second element in the vector,
$$\alpha_2-\alpha_3+2\alpha_4 = 0$$
- and, multiply all the scalars with the third element
$$\alpha_1+\alpha_3-3\alpha_4 = 0$$
equate and represent all the scalars in terms of one common scalar, like
$$\alpha_1 = 5\alpha_4$$
$$\alpha_2 = -4\alpha_4$$
$$\alpha_3 = -2\alpha_4$$
$$\alpha_4 = \alpha_4$$
so, we can do that
$$(\alpha_1,\alpha_2,\alpha_3,\alpha_4) = (5\alpha_4,-4\alpha_4,-2\alpha_4,\alpha_4) \implies \alpha_4(5,-4,-2,1)$$
since now $\alpha_4$ values can be anything like 1 or 2 or 0. This example's a linearly dependent vector (linearly dependent vector may or may not have a zero vector)

### span
a set of vectors that generates the whole vector space.
### line of vector
the set of all scalar multiple of V is called the line of a vector V.
### co-linear
the two vectors V<sub>1</sub> and V<sub>2</sub> are co-linear if they lie on the same line or vector
### the plane of vectors
the two vectors V<sub>1</sub> and V<sub>2</sub> which isn't co-linear. The span of these two vectors is called the plane of these vectors.
### coplanar
the vectors are said to be co-planar, if they lie on the same plane.
### basis
a subset B of vector space V is set to be basis, if it satisfies,
- B is L.I set
- B generates V,that is B is a span of V
the number of vectors in a basis is called dimension of that vector space. AKA dim(V).

- if dim(V) = n, then the vector space is n-dimensional vector space.
	 - if dim(V) isn't finite, V is called infinite dimensional vector space.

## linear transformation or linear map
let u,v be two vector space, then the map
$$ T: u \to v $$
is a linear transformation or linear map if it satisfies,
- $T(u_1+u_2)= T(u_1)+T(u_2)$
- $T(\alpha u_1)=\alpha T(u_1)$
### function
in a mapping, if every element of a domain has a unique image in the co-domain, then that mapping is said to be a function.
#### one-one function
a function in which distinct element in the domain has a distinct image in co-domain.
#### onto function
a function in which every element of the co-domain has a pre-image in the domain. When all of co-domain is equal to range.
#### range and kernel
- in a function, the collection of elements in the co-domain for which there is a pre-image in the domain is called the range. It's a subset of co-domain.
- in a function, the collection of elements in the domain which has an image in co-domain as 0 is called the kernel.

let u,v be two vector spaces, 
$$T: u \to v$$
(read as T is a function from u to v) and (u is domain and v is co-domain)
then,
$$range\ of\ T = R(T) = \{T(x)\ |\ x \in u \}$$
$$kernel\ of\ T = Ker(T) = \{x\ \in u \ |\ T(x) = 0 \}$$
#### rank and kernel
- the dimension of range of T is called the rank of T
	denoted as r(T)
- the dimension of kernel of T is called the nullity of T
	denoted as N(T)

### rank-nullity theorem
let u,v be two vector space,
$$T: u \to v$$
then, 
$$dim(u) = dim(R(T)) + dim(Ker(T))$$
$$ \implies dim(u) = r(T)+ N(T)$$
note
$T: V_3 \to V_3$, here 3 is the dimension number.

eg:
verify rank-nullity theorem for $T: V_2 \to V_3,\ T(x_1,x_2)=(x_1+x_2,x_1-x_2,x_2)$ 
1) to find the range,
$$range(T) = \{T(u)\ | \ u \in U\}$$
$$= \{T(u)\ |\ u \in V_2\}$$
$$= \{T(x_1,x_2)\ |\ (x_1,x_2) \in V_2\}$$
$$\implies \{(x_1+x_2\ ,x_1-x_2\ ,x_2)\}$$
	this vector can be written as,
$$x_1(1,1,0)+x_2(1,-1,1)$$
	therefore the two vectors that generates range is,
$$\{(1,1,0),(1,-1,1)\} \implies r(T) = 2$$
2) to find the kernel,
$$Ker(T) = \{x \in u \ | \ T(x) = 0\}$$
$$ = \{(x_1,x_2) \in u \ | \ T(x_1,x_2) = 0\}$$
$$ = \{(x_1+x_2,x_1-x_2,x_2) \in u \ | \ T(x_1+x_2,x_1-x_2,x_2) = 0\}$$
	now, equate all the elements separately to 0,
$$x_1+x_2 = 0 \to (1)$$
$$x_1-x_2 = 0 \to (2)$$
	then, 
$$x_1 = x_2$$
$$x_2 = 0 \to (3)$$
	so,
$$x_1 = 0$$
	therefore,
$$Ker(T) = \{(0,0)\} \implies N(T) = 0$$

3) verify,
$$dim(u) = r(T) + N(T)$$
$$2 = 2+0 \implies 2=2$$
	.