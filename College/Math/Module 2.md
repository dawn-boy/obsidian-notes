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
$$ F = x^2 + y^3 + x^2 $$
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
