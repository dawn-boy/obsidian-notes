# Big O
![[image/Pasted image 20260112144951.png]]
Big O notations are burdened with the glorious purpose of finding the growth rate of an algorithm relative to the size of the input as `n` grows very large.
The Key idea is to understand how the runtime of an algorithm scales when `n` scales
### `O(n2)`- A loop within a loop
### `O(n)`- Proportional
### `O(logn)`- Divide and Conquer
### `O(1)` - Constant Time
```c++
int addItems(int n){
	return n + n;
}
```
This function yields `O(1)` as only one operation is executed regardless of the value of `n`

if we've had,
```c++
int addItems(int n){
	return n + n + n;
}
```
This function yields `O(2)` as there are two operations. But still its considered under `O(1)`. This is because constants do not influence growth rate significantly like larger inputs.

## Dropping the Non-Dominants
```c++
void printItems(int n){
	for(int i = 0; i < n; i++){             // O(n^2)
		for(int j = 0; j < n; j++){
			cout << i << j << endl;
		}
	}
	
	for(int k = 0; k < n; k++){            // O(n)
		cout << k << endl;
	}
}
```

- in the given example, we have
	- `O(n^2)` and `O(n)` which can be combined and written as `O(n^2 + n)`
So, for larger values of `n`, `n^2` is the dominating term and `n` value becomes less significant.
***
## Big O: `vector`
### Insertion and deletion at the end
![[Pasted image 20260112143604.png]]
![[Pasted image 20260112143626.png]]
Since we're not disturbing other elements from the list, This is just
$$O(1)$$
### Insertion and deletion at the beginning
![[Pasted image 20260112143718.png]]
### The result
![[Pasted image 20260112143906.png]]
![[Pasted image 20260112143837.png]]
Since, inserting or deleting at the beginning messes with the index of all the remaining items in the list.
$$O(n)$$
### Looking up by value
We need to go through all the items to find the needed element, so
$$\implies O(n)$$

### Looking up by index
We can just directly go to the index and find the element, so
$$\implies O(1) $$
***
## Common Data structure operations
![[Pasted image 20260112145132.png]]
### Array sorting algorithms
![[Pasted image 20260112145243.png]]
***
# Linked list
## Singly linked list
![[Pasted image 20260113141257.png]]
### 1. Adding nodes
#### Adding to the front
$$O(1)$$as we just need to move the head pointer
#### Adding to the end
==**If tail node is separately implemented.**== Then its just an action of moving the tail node. Its
$$O(1)$$
==**If tail node is not implemented.**== Then its we have to traverse through the entire list, so
$$O(n)$$
### 2. Removing nodes
#### Removing nodes from the front
$$O(1)$$
as we just need to move the head pointer to the next node.
#### Removing nodes from the end
$$O(n)$$
as we need to iterate through the list to find the last before element to make the tail node point at it.
#### Removing nodes from the middle
$$O(n)$$
as we must first find the node by value and its previous node.
### 3. Accessing the value
#### Access by index
there is no index, so we must traverse through from head
$$O(n)$$
#### Access by value
its a linear scan of entire list
$$O(n)$$
## Comparison with Arrays
![[Theory-1768294782733.jpeg]]
#### Vectors are better at
- Access by index -> `O(1)`
- remove last element -> `O(1)`
- cache friendly as its contiguous memory

#### Singly Linked lists are better at
- Insert and delete at beginning -> `O(1)`
- avoids element shifting
