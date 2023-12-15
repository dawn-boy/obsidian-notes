# Basics
#### Differentiation rules :
$$ Cx = C(x') $$
$$ xy = xy' + x'y $$
$$ x + y = x' + y' $$
$$ \frac{x}{y} = \frac{x'y - xy'}{y^2} $$
$$ f(g(x)) = f'(g(x)) * g'(x) * x'$$
#### Exponential functions :
$$ e^x = e^x $$
$$a^x = a^xln(a)$$
$$e^{g(x)} = e^{g(x)}*g'(x)$$
$$a^{g(x)} =a^{g(x)} * ln(a) * g'(x)$$
#### Logarithmic functions
$$ln(x) = \frac{1}{x}, x>0$$

$$ln(g(x)) = \frac{g'(x)}{g(x)} $$
$$log_ax = \frac{1}{xln(a)}, x> 0 $$
$$log_ag(x) = \frac{g'(x)}{g(x)ln(a) }$$
#### Trigonometry functions 
$$sin(x) = cos(x)$$
$$cos(x) = -sin(x)$$
$$tan(x) = sec^2(x)$$
$$cosec(x) = -cosec(x)cot(x) $$
$$sec(x) = sec(x)tan(x) $$
$$cot(x) = -cosec^2(x)$$
#### Inverse Trigonometry functions
$$sin^{-1} = \frac{1}{\sqrt{1-x^2}} $$
$$cos^{-1} = \frac{-1}{\sqrt{1-x^2}} $$
$$tan^{-1} = \frac{1}{1+x^2} $$
$$cosec^{-1} = \frac{-1}{x\sqrt{x^2-1}} $$
$$sec^{-1} = \frac{1}{x\sqrt{x^2-1}} $$
$$cot^{-1} = \frac{-1}{{1+x^2}} $$

## Functions 
An expression that defines a relation between the two variables
$$y=2x+3 $$
Here, 
y is dependent variable,
x is independent variable.

### Linear function 
Polynomial function with highest degree of 1, 
Straight line on graph.
### Non-Linear function 
Polynomial function with highest degree other than 1,
Not a straight line on graph.
### Existence of limit
$$ \lim_{x \to a} f(x), $$
Limit of f(x) exists only if,
$$ \lim_{x \to a^-}f(x) = \lim_{x \to a^+}f(x) $$
### L'hopital rule
if 0/0 form is obtained while substituting the limit values,

Then, Differentiate the Numerator separately, and the Denominator separately. and put the parts back together. Now cross your fingers and hope it doesn't jinx.

### Continuity
A function is continuous at point C, if
- F(c) is defined,
- $$ \lim_{x \to c}f(x) $$ 
,exists
- $$ \lim_{x \to c}f(x) = f(c) $$
# Partial Derivatives
let F be a function of variables x, y, z,
$$ F = x^2 + y^2 + z^2 $$
Then, Derivative of that function F, is just differentiating the given variable and treating all others as if they're constants.
$$ \frac{\partial{F}}{\partial{x}} = F_x = 2x + 0 + 0 $$
$$ \frac{\partial{F}}{\partial{y}} = F_y = 0 + 2y + 0 $$
$$ \frac{\partial{F}}{\partial{z}} = F_z = 0 + 0 + 2z $$
Now, Double Partial Differentiation, 
$$ \frac{\partial^2{F}}{\partial{x^2}} =F_{xx} = 2 $$
# Jacobians
$$ J(\frac{u,v}{x,y}) = \frac{\partial{(u,v)}}{\partial{(x,y)}} = \begin{vmatrix*} \frac{\partial{u}}{\partial{x}} && \frac{\partial{u}}{\partial{y}} \\ \frac{\partial{v}}{\partial{x}} && \frac{\partial{v}}{\partial{y}} \end{vmatrix*} $$
$$ J(\frac{u,v,w}{x,y,z}) = \frac{\partial{(u,v,w)}}{\partial{(x,y,z)}} = \begin{vmatrix*} \frac{\partial{u}}{\partial{x}} && \frac{\partial{u}}{\partial{y}} && \frac{\partial{u}}{\partial{z}}  \\ \frac{\partial{v}}{\partial{x}} && \frac{\partial{v}}{\partial{y}} && \frac{\partial{v}}{\partial{z}} \\ \frac{\partial{w}}{\partial{x}} && \frac{\partial{w}}{\partial{y}} && \frac{\partial{w}}{\partial{z}}  \end{vmatrix*} $$
## Properties
- let, $$ J = \frac{\partial{(x,y)}}{\partial(u,v)}, J' = \frac{\partial{(u,v)}}{\partial(x,y)} $$
then,
$$ JJ' = 1 $$
- $$ \frac{\partial{(u,v)}}{\partial(x,y)} = \frac{\partial{(u,v)}}{\partial(r,\theta)} * \frac{\partial{(r,\theta)}}{\partial(x,y)} $$
### Qns
- polar or cylindrical cordinates will be given, use jacobian principal and solve it.
# Maxima and Minima of functions of 2 variables
- A Function f(x,y) is said to have a maximum value at the point (a,b), if $$ f(x,y) \le f(a,b) $$
- A Function f(x,y) is said to have a minimum value at the point (a,b), if $$ f(x,y) \ge f(a,b) $$
- The Values of Maximum and Minimum are called the Extreme values of the Function
- critical point is (0,0)

### Lagrange's Method of Multiplication
- Used to determine the maxima and minima values of a function in 2 variables x,y.

#### Steps
- Given,
$$ f(x,y) = xy $$ $$ g(x,y)= 4x^2+y^2-8 $$
- Rewrite the given equations in lagrange form,
$$ F(x,y,\lambda) = f(x,y) + \lambda g(x,y) $$
so, 
$$ F(x,y,\lambda) = xy + \lambda(4x^2+y^2-8) $$
- solve them and equate them to zero,
$$ \frac{\partial{F}}{\partial{x}} = y + \lambda(8x ) = 0, \frac{\partial{F}}{\partial{y}} = x + \lambda(2y) = 0 $$
$$ y = -8\lambda x ,\ x = - 2\lambda y $$
$$ \frac{x}{y} = \frac{-2\lambda y}{-8\lambda x} \implies \frac{y}{x} = \frac{4x}{y} \implies y^2 = 4x^2 \implies y = \pm \ 2x  $$
- substitute the y value in g(x,y),
$$ 4x^2 + y^2 = 8 \implies 4x^2 + 4x^2 = 8 \implies 8x^2 = 8 \implies x = \pm \ 1 \implies y = \pm \ 2$$
- therefore the stationary points are,
$$ (1,2), (-1,2), (1,-2), (-1,-2) $$
- Substitute the stationary points in f(x,y), and whichever gets all time low, it's stationary point is the minima, and all time high's stationary point is maxima.
***
Let,
$$ \vec{A} = 5x\hat{i} + 4y\hat{j} $$
$$ \vec{B} = 2x\hat{i} + 3y\hat{j} $$

then,
## Dot Product
$$ \vec{A} \bullet \vec{B} = (5x)(2x) + (4y)(3y)= 10x^2 + 12y^2  $$
## Cross Product
$$ \vec{A} \times \vec{B} = \begin{vmatrix*} i && j && k \\ 5x && 4y && 0 \\ 2x && 3y && 0 \\ \end{vmatrix*} $$
# Vector Differentiation
Let,
$$ \vec{R} $$
be a vector.
Then, It's Vector Differentiation of R with respect to time (t) is given by,
$$ \frac{d\vec{R}}{dt} $$
### Properties
-  $$ \frac{d(\hat{F} + \hat{G} - \hat{H})}{dt} = \frac{d\hat{F}}{dt} +\frac{d\hat{G}}{dt} - \frac{d\hat{H}}{dt}$$
- $$ \frac{d(\hat{F}\bullet \hat{G})}{dt} = \hat{F}\bullet \frac{d\hat{G}}{dt} + \frac{d\hat{F}}{dt} \bullet \hat{G} $$ 
- $$ \frac{d(\hat{F}\times \hat{G})}{dt} = \hat{F}\times \frac{d\hat{G}}{dt} + \frac{d\hat{F}}{dt} \times \hat{G} $$ 
- $$ \frac{d(\hat{F}\phi)}{dt} = \hat{F}\times \frac{d\phi}{dt} + \frac{d\hat{F}}{dt} \times \phi $$ 
- Differentiation of a Constant vector is 0
- $$ \hat{F} \bullet \frac{d\hat{F}}{dt} = 0 $$
- $$ \hat{F} \times \frac{d\hat{F}}{dt} = 0 $$
# Curves in Space

## Tangent
$$ r(t) = x(t)\hat{i} + y(t)\hat{j} + z(t)\hat{k} $$
## Curvature
The arc rate of change of tangent 
$$ \frac{dt}{ds} = \kappa  $$
## Torsion
The arc rate of change of binormal
$$ \frac{dB}{dS} = \tau $$
### Note

- reciprocal of curvature is radius of curvature, $$ \rho = \frac{1}{\kappa} $$
- reciprocal of torsion is radius of torsion,$$ \sigma = \frac{1}{\tau} $$
- $$ \kappa = \frac{|r'(t) \times r''(t)|}{|r'(t)|^3} $$
- $$ \tau = \frac{(r'(t) \times r''(t)) \bullet r'''(t) }{|r'(t) \times r''(t)|^2} $$
- Torsion of a Plane Curve is 0

## Angle between the vectors
Angle between the vectors
$$ \theta = cos^{-1}( \frac{\vec{a} \bullet \vec{b}}{|\vec{a}||\vec{b}|}) $$
## Velocity and Acceleration

$$ speed = \frac{distance}{time} $$
$$ velocity = \frac{displacement}{time} $$
$$ acceleration = \frac{velocity}{time} $$
Let R be a Positional Vector, then, 
- Velocity is R'(x) $$ \vec{V} = \frac{d\hat{R}}{dt}  $$
- speed is the magnitude component of Velocity $$ S = \vec{|V|}  $$
- Acceleration is the rate of change of velocity, so V'(x)$$ \vec{A} = \frac{d\vec{V}}{dt} $$
- To find the component of A(vec) in the direction of B(vec), $$ \frac{\vec{A}\bullet\vec{B}}{|\vec{B}|} $$
## Vector differential Operation
Let Phi be a scalar, then,
$$ gradient = \nabla\phi = grad\phi = \frac{\partial{\phi}}{\partial{x}} \hat{i} +\frac{\partial{\phi}}{\partial{y}} \hat{j} +\frac{\partial{\phi}}{\partial{z}} \hat{k}   $$
- Maximum value of Phi is, $$ \implies |\nabla\phi| $$
- directional derivative of phi in direction of vector a, $$ \implies \frac{\nabla\phi \bullet \vec{a}}{|\vec{a}|} $$
- unit normal of gradient, $$ \frac{\nabla\phi}{|\nabla\phi|} $$
- Angle between two surfaces, $$ \theta = cos^{-1}( \frac{\nabla\phi_1 \bullet \nabla\phi_2}{|\nabla\phi_1||\nabla\phi_2|}) $$
- phi(1) and phi(2) are orthogonal to each other if, $$ \nabla\phi_1 \bullet \nabla\phi_2 = 0 $$
## Divergent vector
The amount of flow entering or exiting a point
$$ \nabla \bullet \vec{F} = (\frac{\partial{}}{\partial{x}}\hat{i} + \frac{\partial{}}{\partial{y}}\hat{j} + \frac{\partial{}}{\partial{z}}\hat{k}  ) \bullet (\hat{f_1} + \hat{f_2} + \hat{f_3}) $$
$$ \implies \frac{\partial{f_1}}{\partial{x}}\hat{i} + \frac{\partial{f_2}}{\partial{y}}\hat{j} + \frac{\partial{f_3}}{\partial{z}}\hat{k}  $$
- if a flow is exiting a point, then it is Positive divergence
- if a flow is entering a point, then it's a Negative divergence

==for a Solenoidal vector, $$ \nabla \bullet \vec{F} = 0 $$==
## Curl vector
the amount of rotation
$$ \nabla \times \vec{F} = \begin{vmatrix*} \hat{i} && \hat{j} && \hat{k} \\
\frac{\partial}{\partial{x}} && \frac{\partial}{\partial{y}} && \frac{\partial}{\partial{z}} \\ f_1 && f_2 && f_3 \end{vmatrix*} $$
==for a irrotational vector,==
$$  \nabla \times \vec{F} = 0 $$
***

# Integration

## formulas

| Basic | Trigonometry | Inverse Trig |
| ----- | ------------ | ------------ |
| $$ \int{cf(x)\;dx} = c\int{f(x)\;dx} $$ | $$ \int{sin(x) \;dx} = -cos(x) + c $$ | $$ \int{\frac{1}{\sqrt{1-x^2}} \;dx} = sin^{-1}(x) + c $$|
| $$ \int{k\;dx} = kx + c $$      | $$ \int{cos(x) \;dx} = sin(x) + c $$ | $$ \int{\frac{-1}{\sqrt{1-x^2}} \;dx} = cos^{-1}(x) + c $$|
| $$ \int{x^n\;dx} = \frac{x^{n+1}}{n+1} + c $$ | $$ \int{tan(x) \;dx} = -log(cos(x)) + c $$ | $$ \int{\frac{1}{1+ x^2} \;dx} = tan^{-1}(x) + c $$ |
| $$ \int{e^x \;dx} = e^x + c $$      | $$ \int{cosec(x) \;dx} = -log(cosec(x) + cot(x)) + c $$ | $$ \int{\frac{-1}{x\sqrt{x^2-1}} \;dx} = cosec^{-1}(x) + c $$|
| $$ \int{\frac{1}{x} \;dx} = log(x) + c $$| $$ \int{sec(x) \;dx} = log(sec(x) + tan(x)) + c $$ |$$ \int{\frac{1}{x\sqrt{x^2-1}} \;dx} = sec^{-1}(x) + c $$ |
| $$ \int{ f(x) + g(x) \;dx} = \int{f(x) \;dx} + \int{g(x) \;dx} + c $$ | $$ \int{cot(x) \;dx} = -log(sin(x)) + c $$ | $$ \int{\frac{-1}{1+ x^2} \;dx} = cot^{-1}(x) + c $$|
| $$ \int{a^x \;dx} = \frac{a^x}{log(a)} + c $$| $$ \int{cosec^2(x) \;dx} = -cot(x) + c $$ |              |
| $$ \int{\frac{f'(x)}{f(x)} \;dx} = log(f(x)) + c $$| $$ \int{sec^2(x) \;dx} = tan(x) + c $$             |              |
| $$ \int{f(x)^n \bullet f'(x) \;dx} = \frac{f(x)^{n+1}}{n+1} + c $$| $$ \int{sec(x)tan(x) \;dx} = sec(x) + c $$ | |
| | $$ \int{cosec(x)cot(x) \;dx} = -cosec(x) + c $$ | |


## integration by symmetric functions
## even functions
- a function is said to be even, if, $$ f(-x) = f(x) $$
$$ \implies 2\int^a_{0}{f(x) \;dx} $$
## odd functions
- a function is said to be odd, if, $$ f(-x) = -f(x) $$
$$ \implies \int^a_{-a}{f(x) \;dx} = 0 $$
## integration by parts
ILATE = Inverse trigonometry, Logarthmic, Algebraic, Trigonometry, Exponential
$$ \int{u \;dv } = uv - \int{v \;du} $$
# Bernollins Formula 
$$ \int{u \;dv} = uv_1 +u'v_2 + u''v_3 - u'''v_4 $$
differentiate until there's only constant left in u term.
Differentiating u and integrating v
