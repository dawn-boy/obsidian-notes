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
- Eigen Values of Matrix A = Eigen Values of Matrix A transpose
- for upper and lower triangular matrices, the Eigen Values are it's diagonal elements 
- Sum of Eigen Values = Sum of Diagonal values
- Product of Eigen Values = Determinant of Matrix A
- for Idemponet matrix (A<sup>2</sup> = A), Eigen Values is 1 or 0
- Eigen Values of 
		- KA --> Kλ<sub>1</sub>, Kλ<sub>2</sub>, ... ,Kλ<sub>n</sub>
		- A<sup>P</sup> --> λ<sub>1</sub><sup>P</sup>, λ<sub>2</sub><sup>P</sup>, λ<sub>3</sub><sup>P</sup>
		- A<sup>-1</sup> --> 1/λ<sub>1</sub>, 1/λ<sub>2</sub>, 1/λ<sub>3</sub>
***
## Cayley-hamilton theorem 
It states that every matrix must satisfy its own characteristics equation.
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
