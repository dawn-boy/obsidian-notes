# Big O
![[Pasted image 20260112144951.png]]
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