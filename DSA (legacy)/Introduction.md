# Data structures
they are different ways of organizing data on your computer so that they can be used effectively.
## Algorithms
They are a set of steps to accomplish a task. They need to be,
- Efficiency 
- Correctness
==If we take a library as an example, then
the Books are the data,
The Library is the data-structure,
Searching for a book is an algorithm==
# Types of Data Structures 
They are grouped based on two types,
# 1. Primitive Data structures
which is predefined in the programming language
## Static 
- arrays
## Dynamic
- Linked lists
- Stacks
- Queue 
## 2. NonPrimitive data structures
Non-Primitive data structures are derived from primitive data structures by combining two are more primitive data structures.
- Tree
- Graphs 
# Types of Algorithm
1. Simple Recursive algorithms
2. Divide and conquer algorithms
3. Dynamic programming algorithms
4. Greedy algorithms
5. Brute force algorithms
6. Randomized algorithms
***
# What is Big O
Big O is a language and metric that's used to describe the efficiency of the algorithm
## Time complexity
Its a way of showing how the runtime of a function increases as the size of the input increases.
==It Time complexity we don't look at how much time the code takes to run because that factor varies with a faster computer. So, instead we look at the number of operations within the algorithm.==
## Space complexity
The amount of space consumed by that algorithm 
# Big O notations
So,
- Big $\Omega$ => Best case scenario
	Its the complexity that's atleast or more than the best case
- Big $\Theta$ => Average case scenario
	It's the complexity that's within the bounds of Worst and best case
- Big O => Worst case scenario
	Its the complexity that's less or equal to the worst case
## Runtime complexities
## O(1) - Constant 
Its the most efficient time complexity, nothing is more efficient than the constant time complexity
### Example
```java
class Main{
	public static void printSquare(int n){
		for(int i=0; i<n; i++){
			System.out.println(i**2)
		}
	}
	public static void main(String[] args){
		printSquare(20)
	}
}
```
## O(N) - Linear
### Example
```java
class Main{
	public static void printNumbers(int n){
		for(int i=0; i<n; i++){
			System.out.println(i)
		}
	}
	public static void main(String[] args){
		printNumbers(200);
	}
}

// output
0
1 
...
199
```

if we had two for loops within the `printNumbers` function,
```java
class Main{
	public static void printNumbers(int n){
		for(int i=0; i<n; i++){             // N complexity
			System.out.println(i)
		}
		for(int j=0; j<n; j++){            // N Complexity
			System.out.println(j)
		}
	}
	public static void main(String args[]){
		printNumbers(100)                  // Evaluates to 2N complexity
	}
}
```
Now this evaluates to `O(2n)` but we ignore the constants because they just lots of noise from hardwares and has small changes in the algorithm that isn't important for the analysis
## O(LogN) - Logarthmetic
## O(N<sup>2</sup>) - Quadratic 

## Rules to decide on the time Complexity

| Rules | Description                                                          | Complexity       |
| ----- | -------------------------------------------------------------------- | ---------------- |
| 1.    | Any assignment statements and if statements that are executed once   | O(1)             |
| 2.    | A Simple for loop from 0 to n (with no nested loops)                 | O(n)<br>         |
| 3.    | A Nested loop of the same type                                       | O(n<sup>2</sup>) |
| 4.    | A Loop with a controlling parameter that's dividing by two each step | O(log n)<br>     |
| 5.    | When dealing with multiple statements, just add them up              |                  |
```java
public static void summation(int n){
	var total = 0;                         // O(1)
	for(int i = 0; i <= n; i++){           // O(n)
		total += i                         // O(1)
	}
	if(i > 100){                           // O(1)
		System.out.println("The summation is more than 100")   // O(1)
	}
	else{                                     // O(1)
		System.out.println(total)             // O(1)
	}
}
```
So the final time complexity is 
$$O(1) + O(n) + O(1) + O(1) +O(1) + O(1)  + O(1) \implies O(n) $$
