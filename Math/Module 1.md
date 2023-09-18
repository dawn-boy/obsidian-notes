***
# Matrix basics
$$ A= \begin{bmatrix} a & b & c \\ d & e & f \\ g & h & i\end{bmatrix}$$
#### Minor of A<sub>11</sub>
$$ M_{11} = \begin{vmatrix*} e & f \\h & i \end{vmatrix*}$$
#### Determinant of A
$$ a*\begin{vmatrix*} e & f \\ h & i \end{vmatrix*}- b* \begin{vmatrix*} d&f\\ g&i\end{vmatrix*}+c*\begin{vmatrix*} d & e \\ g & h \end{vmatrix*}$$
#### Cofactor of A
$$ C_{ij} = (-1)^{ij}*M_{ij} $$
#### Adjoint of A
$$ Adj(A) = C^T$$
#### Inverse of A
$$ A^{-1} = 1/\begin{vmatrix*}A\end{vmatrix*}*Adj(A) $$

***
## characteristics equations
#### 2x2 matrix
$$ \lambda^2 - S_1\lambda + S_2 = 0 $$
Where, 
S<sub>1</sub> --> sum of diagonal elements,
S<sub>2</sub> --> determinants of the matrix.

#### 3x3 matrix
$$ \lambda^3 - S_1\lambda^2 + S_2\lambda - S_3 = 0 $$
Where,
S<sub>1</sub> --> sum of diagonal elements,
S<sub>2</sub> --> sum of minors of the diagonal elements,
S<sub>3</sub> --> determinant of the matrix.

## Eigen Vectors equation
$$ (A-\lambda I)\vec{X} = \vec{0} $$
***
## Find Eigen Values
#### 2x2
- find S<sub>1</sub>, S<sub>2</sub>
- factorise the resulting equations and find λ<sub>1</sub> and λ<sub>2</sub>
- compute for λI and find the X vector using the vector equation
#### 3x3
- find  S<sub>1</sub>, S<sub>2</sub>, S<sub>3</sub>
- guess the value of λ<sub>1</sub> by trial and error method
- get a quadratic equation and solve for λ<sub>2</sub> and λ<sub>3</sub>
- compute for λI and find the X vector for each Eigen Values
***
## Properties of Eigen Values and Vectors
- for upper and lower triangular matrices, the Eigen Values are it's diagonal elements 
- Sum of Eigen Values = Sum of Diagonal values
- Product of Eigen Values = Determinant of Matrix A
- for Idemponet matrix (A<sup>2</sup> = A), Eigen Values is 1 or 0
- Eigen Values of 
		- KA --> Kλ<sub>1</sub>, Kλ<sub>2</sub>, Kλ<sub>n</sub>
		- A<sup>P</sup> --> λ<sub>1</sub><sup>P</sup>, λ<sub>2</sub><sup>P</sup>, λ<sub>3</sub><sup>P</sup>
		- A<sup>-1</sup> --> 1/λ<sub>1</sub>, 1/λ<sub>2</sub>, 1/λ<sub>3</sub>
		- A<sup>T</sup> --> λ<sub>1</sub>, λ<sub>2</sub>, λ<sub>3</sub>
***
## Cayley-hamilton theorem 
It states that every matrix must satisfy it's own characteristics equation.
Let A be the matrix
#### 2x2 matrix
$$ A^2 - S_1A + S_2I = 0 $$
#### 3x3 matrix
$$ A^3 - S_1A^2 + S_2A - S_3I = 0 $$
***
## Similar matrices
Two matrix A and B are said to be similar if there exist a matrix P such that 
$$ B = P^{-1} A P$$
### Diagonalization of matrix
Diagonalization is a process of reducing any matrix A into its diagonal form D. 
As per the similarity transformation, If A is related to D, then
D = P<sup>-1</sup>AP (where P is a modal matrix consisting of Eigen vectors of A)

==Note:
$$ D = P^{-1}AP $$
$$A=PDP^{-1}$$
$$A^n=PD^nP^{-1}$$
D is made up of Eigen Values of A, whereas
P is made up of Eigen vectors of A. Thus so to eloquently put it.==

### Steps to Diagonalize
- find the Eigen Values and Eigen vectors of the matrix
- check if the Eigen vectors are linearly independent (not same to one another)
- form P from the Eigen vectors
- find P and P<sup>-1</sup> to satisfy D = P<sup>-1</sup>AP 
- D is the required diagonal form containing the Eigen Values of A
***
# What is the Quadratic form?
A Homogeneous equation (all variables have equal power) of 2nd degree in any number of equation.
## What is it's Canonical form?
The sum of it's square terms (Principal axis form)

$$ ax^2 + by^2 + cz^2 + 2fxy + 2gyz + 2hzx $$

$$ \begin{bmatrix} a & f & h \\ f & b & g \\ h & g & c\end{bmatrix}$$
- coefficient of the squares are on the diagonal,
- coefficient of the other terms are split between it's two sides.
## Orthogonal vectors
Two vectors are said to be orthogonal if they satisfy,
$$ X^TY = 0 $$
### Orthogonal transformation
Transforming a quadratic equation to it's canonical form using,
$$ D = P^TAP $$
where P is a normalized vector.
## Normalized vector
To Normalize the vector A,
$$ A = \begin{bmatrix} a \\ b \\ c \end{bmatrix}$$
We gotta,
$$ x = \sqrt{a^2 + b^2 + c^2} $$
Then, divide the whole matrix by x,
$$ A = \begin{bmatrix} a_{/x} \\ b_{/x} \\ c_{/x} \end{bmatrix}$$
Now A is a normalized matrix.

#### To Convert a quadratic equation to it's Canonical form using Orthogonal transformation
- convert the Quadratic equation to it's Matrix form
- Solve for it's Eigen Values and Eigen Vectors 
- check if the Eigen vectors are orthogonal to each other
- Normalize the Eigen vectors
- Form the matrix P from the normalized Eigen vectors
- find D using the Orthogonal transformation formula 
==(Do not, even in life or death situation, multiply P with P<sup>T</sup> at first. GO WITH P<sup>T</sup> AND A OR P WITH A)==
## Nature of Quadratic form
- Rank (r) of a Matrix A = number of positive and negative eigen Values. 
If that matrix A has a quadratic form Q that satisfies,
$$ Q = X^TAX $$
- Index (p) of a quadratic form = number of Positive eigen values 
- Signature (s) of a quadratic form = Postive eigen values - Negative eigen values.
### A Quadratic form is said to be
- Postive Definite - All Eigen values are postive and greater than zero,
- Positive SemiDefinite - All Eigen values are positive and atleast one of them is zero,
- Negative Definite - All Eigen values are negative and less than zero,
- Negative SemiDefinite - All Eigen values are negative and atleast one of them is Zero,
- Indefinite - Negative and positive eigen values.

## Finding Nature of a quadratic equation using Determinants

Let there be a matrix A,
$$ A = \begin{bmatrix} a & b & c \\ d & e & f \\ g & h & i \end{bmatrix}$$
Then d<sub>1</sub>, d<sub>2</sub>, d<sub>3</sub> are
$$ d_1 = a$$
$$ d_2 = \begin{vmatrix*} a & b \\ d & e \end{vmatrix*}$$
$$ d_3 = \begin{vmatrix*} a & b & c \\ d & e & f \\ g & h & i\end{vmatrix*} $$
- Positive Definite - d<sub>i</sub> > 0,
- Positive SemiDefinite - d<sub>i</sub> >= 0,
- Negative Definite - d<sub>1</sub>,d<sub>3</sub>,d<sub>5</sub> is negative and d<sub>2</sub>,d<sub>4</sub>,d<sub>6</sub> is positive and all are > 0,
- Negative SemiDefinite - d<sub>1</sub>,d<sub>3</sub>,d<sub>5</sub> is negative and d<sub>2</sub>,d<sub>4</sub>,d<sub>6</sub> is positive and all are >= 0
- Indefinite - anything else.
***
# Complex Matrix
If the elements of the matrix A are complex numbers, then the Conjugate of the Matrix is,
$$ conjugate(A) = \overline{A} $$
Transpose of the conjugate is,
$$ (\overline{A})^T = A^\theta = A^* $$
## Hermitian Matrix
A square matrix A that satisfies,
$$ A^T = \overline{A} $$
## Skew-Hermitian Matrix
A square matrix A that satisfies,
$$ A^T = -\overline{A} $$
### Properties 
- Any square matrix can be written as the sum of it's Hermitian Matrix and Skew-Hermitian Matrix.
- if A is Hermitian Matrix then iA is Skew-Hermitian Matrix
- Eigen values of Hermitian Matrix = real numbers
- Eigen values of Skew-Hermitian Matrix = imaginary or zero
## Unitary Matrix
A Matrix A is said to be unitary matrix if it satisfies,
$$ A^{-1} = (\overline{A})^T = A^* $$


