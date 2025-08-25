Main datatype in Numpy is `ndarray` -> n-dimensional array
# Creating arrays
1. The Manual Way
2. Pre-filled values
3. Evenly spaced values
4. Random integer arrays
## 1. The Manual way
```python
a1 = np.array([1, 2, 3])           
a2 = np.array([[1, 2, 3], [4, 5, 6.5]])   
a3 = np.array([
    [[1, 2, 3], [4, 5, 6], [7, 8, 9]],
    [[10, 11, 12], [13, 14, 15], [16, 17, 18]]
])   
```
## 2. Creating pre-filled arrays
### Filled with ones
```python
ones = np.ones((2,4))
```
### Filled with zeroes
```python
zeroes = np.zeroes((3,5))
```
## 3. Evenly spaced
```python
range_array = np.arange(0, 10, 2) # start, stop, step
# Output: [0 2 4 6 8]
```
## 4. Random arrays
To Fix the randomness, use
```python
np.random.seed(3)
```
### Random integers
```python
rand_int_array = np.random.randint(0, 10, size=(3,5)) # start, stop, size
```
- returns integers in `[0, high)`
### Random Float between 0 and 1
```python
rand_array = np.random.random((5,4)) # size
```
- returns float in `[0, 1)`
Normally distributed random numbers
```python
np.random.randn(shape)
```
Evenly spaced
```python
np.linspace(start, stop, step)
```
## Key attributes
- `.shape` -> Gives the dimensions 
- `.ndim` -> The Number of dimensions
- `.dtype` -> datatype of the elements
- `.size` -> Total number of elements
- `type(array)` => `numpy.ndarray` -> gives the python object
***
# Viewing arrays
- finding unique elements
- Terminology
- Indexing and Slicing
## Finding unique elements
```python
np.unique(array)
```
- returns a sorted One-dimensional array
## Terminology
### Array - Numpy's core datatype `numpy.ndarray`
### Vector - An Array with One-dimension
### Matrix - An Array with more than one-dimension

## Indexing and Slicing
### Indexing
#### For 1D
```python
A1[0]       #first element
```
#### For 2D
```python
A2[0]       #first row
```
#### For 3D
```python
A3[0]       #first matrix
```
### Slicing
```python
A3[:, :2, :2]
```
- `:` -> takes all the element across that axis
- `:2` -> takes first two elements across that axis
***
# Arithmetic operations 
- For one dimensional array
- For Multi dimensional array

## Basic Arithmetic
```python
import numpy as np

a1 = np.array([1,2,3])
ones = np.ones((1,3))
```

we can,
```python
A1 + ones   # elementwise addition: [2., 3., 4.]
A1 - ones   # subtraction: [0., 1., 2.]
A1 * ones   # multiplication: [1., 2., 3.]
A1 / ones   # division: [1., 2., 3.]
A1 // ones  # floor division: [1., 2., 3.]
A1 ** 2     # power: [1, 4, 9]
np.square(A1) # same as above
```
## Multi-dimensional array
If the shapes of both the arrays match, then we can proceed with all the usual arithmetic operations
```python
a1 = np.random.randint(1,10,size=(3,3))
ones = np.ones((3,3))

# we can
a1 + ones
```
==But if the shapes mismatch, then we can try broadcasting.==
## Broadcasting
Its a try at uplifting an array to its higher dimension counterpart
### Broadcasting rules
1. If the dimensions are equal, then they're compatible
2. If some part of the dimension has `1`, like
		`(1,3)` or `(3,1)`
	then it is stretched (broadcasted) to match the other

#### Examples
## ==Note==
### **`(3,)` is not the same as `(1,3)`**
```python
[1,2,3] # shape: (3,)
```
its just an array with 3 elements, there's no concept of rows or columns here. JUST THREE ELEMENTS.

```python
[
	[1,2,3]
]

# shape: (1,3)
```
This is an array also with 3 elements, but with `1` row and `3` columns

1. Simple scalar broadcasting
```python
a = np.array([1,2,3])
b = 2

a + b # result: [3,4,5]
```
- here `b` is scalar with `shape: ()`, so its broadcasted to `shape: (3,)`

2. Row + Column vector
```python
a = np.array([[1], [2], [3]]) # shape: (3,1)
b = np.array([5,5,5]) # shape: (3,)
```
- so we broadcast the lower dimensions of `b` with `shape: (3,)` to match `a` 
	so b shape will be: `(1,3)`
So they expand to `(3,3)` without memory duplication

**==If the dimensions mismatch and also neither part has 1 in their shape. Then those arrays are incompatible with each other==**
***
## Aggregation
```python
np.sum(array)
np.mean(array)
np.max(array)
```
Always use the `numpy` functions for arrays instead of python's aggregation functions. `numpy` functions are way faster in these use cases.
***
# Variance and Standard Deviation
## Variance
It tells us how far, on average, each element is from the center (mean)
### Mathematical interpretation
Say we have
```python
[2, 4, 6, 8, 10]
```

1. We find the mean,
$$mean = (2,4,6,8,10) / 5 \implies 6$$
2. We find how far each number is from mean,
$$2 \rightarrow -4$$
$$4 \rightarrow -2$$
$$6 \rightarrow 0$$
$$8 \rightarrow 2$$
$$10 \rightarrow 4$$
3. Square the differences
	so that negatives cancels out
$$ [16, 4, 0, 4, 16]$$
4. Find the average of those squares
$$variance = (16,4,0,4,16)/5 \implies 8$$
So on average, each element is 8 units away from the center or mean.

***==But Variation is on squared unit terms. The same value but unsquared will be on similar units with the given data. This is Standard deviation==***
## Standard deviation
The Square root of variation is Standard deviation. This is to get the spread value on the same units with the given data.

$$std = \sqrt{8} \implies 2.83$$

```python
import numpy as np

# Two arrays: one with big jumps, one with small steps
high_var_array = np.array([1, 100, 200, 300, 4000, 5000])
low_var_array = np.array([2, 4, 6, 8, 10])

# Variance
print(np.var(high_var_array))  # Big number
print(np.var(low_var_array))   # Small number

# Standard deviation
print(np.std(high_var_array))  # Bigger SD
print(np.std(low_var_array))   # Smaller SD

# Mean
print(np.mean(high_var_array))
print(np.mean(low_var_array))
```
***
# Reshape and Transpose
```python
arr.reshape(1,2) # reshapes to given shape
arr.T            # flips the col to rows and rows to cols
```
Transpose is useful during the calculation of dot products
# Dot Product
For Calculating the dot product, the inside dimensions of the shape must match 
$$(M \times n) \cdot (n \times P) \rightarrow (M \times P)$$
![[Numpy-1754824430397.png]]
***
## Comparison operators
```python
import numpy as np

a1 = np.array([1, 2, 3])
a2 = np.array([1, 2, 3.3])

```

```python
# greater than
a1 > a2
# Output: [False False False]

a1 >= a2
# Output: [ True  True False]

a1 > 5
# Output: [False False False]

a1 < 5
# Output: [ True  True  True]

a1 == a2
# Output: [ True  True False]

# we can also combine operators with 
np.logical_and(a1 > 1, a1 < 3)
# Output: [False  True False]

np.logical_or(a1 > 1, a1 < 3)
# Output: [True  True True]
```
## Sorting with `np.sort()`
```python
np.sort(random_array)

# getting just the indices of the sort
np.argsort(random_array)
```

## Min and max index
```python
np.argmin(a1)
np.argmax(a1)

# axis = 0 for column
# axis = 1 for row 
```