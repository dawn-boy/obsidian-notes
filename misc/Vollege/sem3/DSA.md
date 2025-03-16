## Data
collection of raw facts
## information
Information is processed data
## types of datatype
### primitive datatype
- simple and built-in datatypes
- ex: int, char, float, double
### Non primitive datatype
- derived from primitive datatype
- ex: Array, structure, etc
# Data structures
Storing and organizing set of related data computer memory, so they can be accessed efficiently
### types
1. Linear
	1. array
	2. linked list
	3. stack 
	4. queue
2. Non-linear
	1. tree
	2. graphs
	3. tables
	4. sets
### operations
1. traverse
2. insert
3. delete
2. search 
3. sort
4. merge
## Abstract data type (ADT)
- collection of data with its type and operations that can be performed
- abstraction means separating necessary information from unnecessary information
## Linked list
- linked list is a simple, fundamental, recursive data structure that is used everywhere
- it can implement queue and stack
- ex: in web-browser, when you press the back button, the prev page is loaded from the previous node in an linked list
### Data structure applications
- to reverse a word, you push the word into a stack, letter by letter, and then pop the letters from the stack.
- example: the undo mechanism in text editors.
***
# Performance evaluation
#### types
1. Priori analysis - performance analysis
2. Posteriori analysis - performance measurement
### types of spaces
- instruction space
- stack space
- data space
## space complexity 
- the amount of memory needed for the algorithm to run.
- Space S needed for an Algorithm P is taken as the sum of 
	- fixed part - part of code that doesn't change, constants
	- variable part - part of code that depends on user input
- space complexity of an algorithm can be said as s(algo_name)
example:
```
algorithm Sum(a[], n){
	s = 0;
	for i = 1 to n, do:
		s += s + a[i];
	return s
}
```
- s(Sum) >= n + 3
	- array a[] has n elements, 
	- 3 for each variable used. i, s, a.
	- so n + 3
### space efficiency
- it is measured by counting the number of extra memory units used up by the algorithm.
## time complexity
- the amount of time required for the algorithm to run.

examples:
```
for(i=0; i < n; i++){
statement;                          \\ O(n)
}

for(i=0; i < n; i++){
	for(j=0; j < n; j++){
		statement;                   \\ O(n^2)
	}
}

function sum(n)
int sum = 0;
for (int i=1; i<=n; i++)              \\ O(n)
sum = sum + i;
return sum;

for(i=1; i < n; i= i*2){
statement;                             \\ O(log n)
}
```
## recursion vs iteration
- recursion is a function that calls itself. 
- The case where the function does not recur is called the base case.
- The case where the function calls itself to perform a subtask is called the recursive case
```
if (condition){
\\ base case
}
else{
\\ recursive case
}
```

- each recursive call requires extra space, if we get infinite recursion, program may run out of memory.
***
## Linked lists
- Storing elements in array has limitations like fixed array size. So, if you need to extend the array, you have to create a new array and transfer all the elements over. 
- Linked list is a collection of nodes that stores data and links to other nodes.
- These nodes can be present anywhere in the memory.
- The first node is called the head and the last is called the tail.
## single linked list
```c
#include <stdio.h>
#include <stdlib.h>

struct Node{

    int data;
    struct Node *next;
}Node;

struct Node* createNode(int data){
    struct Node* temp = (struct Node*) malloc(sizeof(struct Node));
    temp -> data = data;
    temp -> next = NULL;
    return temp;
}

void insert(int data, struct Node* prevNode){
    struct Node* nextNode = prevNode -> next;
    prevNode -> next = createNode(data);
    prevNode -> next -> next = nextNode;
}
void delete(struct Node* prev, struct Node* del){
    prev -> next = del -> next;
}

void printList(struct Node* list){
    struct Node* temp = list;
    while(temp != NULL){
        printf("%d\n",temp->data);
        temp = temp -> next;
    }
}

int main(){
    
    struct Node* head = createNode(0);
    
    struct Node* n1 = createNode(5);
    struct Node* n2 = createNode(6);
    struct Node* n3 = createNode(7);
    struct Node* n4 = createNode(8);
    
    head -> next = n1;
    n1 -> next = n2;
    n2 -> next = n3; 
    n3 -> next = n4;
    
    printList(head);
    
    printf("\n");
    insert(44, n3);
    delete(n2, n3);
    
    printList(head);
    
}
```

## double linked list
```
#include <stdio.h>
#include <stdlib.h>

struct Node{
    struct Node *prev;
    int data;
    struct Node *next;
}Node;

struct Node* createNode(int data, struct Node* prev){
    struct Node* temp = (struct Node*) malloc(sizeof(struct Node));
    
    temp -> prev = prev;
    temp -> data = data;
    temp -> next = NULL;
}

void display(struct Node* head){
     struct Node* temp = head;
     while (temp != NULL){
         printf("%d", temp-> data);
         temp = temp -> next;
         printf("\n");
     }
}
    
void insert(int data, struct Node* node){
     struct Node* prevNode = node -> prev;
     struct Node* newNode = createNode(data, NULL);
     
     prevNode -> next = newNode;
     newNode -> prev = prevNode;
     newNode -> next = node;
     node -> prev = newNode;
}
void delete(struct Node* node){
    struct Node* prevNode = node -> prev;
    struct Node* nextNode = node -> next;
    
    prevNode -> next = nextNode;
    nextNode -> prev = prevNode;
}


int main(){
    struct Node* head = createNode(0,NULL);
    struct Node* n1 = createNode(2,head);
    struct Node* n2 = createNode(3,n1);
    struct Node* n3 = createNode(4,n2);
    
    head -> next =  n1;
    n1 -> next = n2;
    n2 -> next = n3;
    insert(34,n2);
    delete(n2);
    
    display(head);
}
```
## stack adt
```c
#include <stdio.h>
#include <stdbool.h>

int top = -1;
int max = 10;

bool isFull(){
    return (top == max-1);
}
bool isEmpty(){
    return (top == -1);
}

void push(int data, int stack[]){
    if(!isFull()){
        top++;
        stack[top] = data;
        printf("Added %d to stack! at %d\n", data, top);
    }
    else{
        printf("Stack Overflow!\n");
    }
}
int pop(int stack[]){
    if(!isEmpty()){
        top--;
        return stack[top+1];
    }
    else{
        printf("Stack Underflow\n");
        return 0;
    }
}

void display(int stack[]){
    for(int i=0; i<=top; i++){
        printf("\n%d",stack[i]);
    }
}

void peek(int stack[]){
    if(!isEmpty()){
        printf("\n%d", stack[top]);
    }
    else{
        printf("Stack is empty.");
    }
}

int main(){
    int stack[max];

    push(5,stack);
    push(6,stack);
    push(7,stack);
    push(8,stack);
    push(9,stack);
    push(10,stack);
    push(11,stack);
    push(12,stack);
    push(13,stack);
    push(17,stack);

    display(stack);
    pop(stack);
    peek(stack);
    
}
```

## stack using linked list
```c
#include <stdio.h>
#include <stdlib.h>

int top = -1;
int max = 3;

struct Node {
    int data;
    struct Node* next;
}Node;

struct Node* createNode(int data){
    struct Node* node = (struct Node*) malloc(sizeof(struct Node));
    node -> data = data;
    node -> next = NULL;
    
    return node;
}

void display(struct Node* node){
    struct Node* temp = node;
    while(temp != NULL){
        printf("\n%d",temp -> data);
        temp = temp -> next;
    }
}

void push(int data, struct Node* head){
    top++;
    if(top == max-1){
        printf("Stack Overflow");
    }
    else{
        struct Node* node = createNode(data);
        node -> next = head -> next;
        head -> next = node;
    }
}

void pop(struct Node* head){
    top--;
    if(head -> next != NULL){
    head -> next = head -> next -> next;
    }
    else{
        printf("Stack underflow");
    }
}

int main(){
    
    struct Node* head = createNode(0);

    push(5,head);
    push(6,head);

    pop(head);

    display(head);
}

```
## queue using linked list
```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
}Node;

int top = -1;
int max = 10;

struct Node* createNode(int data){
    struct Node* node = (struct Node*) malloc(sizeof(struct Node));
    node -> data = data;
    node -> next = NULL;
    
    return node;
}

void display(struct Node* node, struct Node* tail){
    struct Node* temp = node;
    while(temp != tail){
        printf("\n%d",temp -> data);
        temp = temp -> next;
    }
}

void enqueue(int data, struct Node* tail){
    top++;
    if(top == max-1){
        printf("Queue overflow");
    }
    else{
        struct Node* node = createNode(data);
        tail -> next -> next = node;
        node -> next = tail;
        tail -> next = node;
    }
}

void dequeue(struct Node* head){
    top--;
    if(top == -1){
        printf("Empty Queue");
    }
    else{
        head -> next = head -> next -> next;
    }
}

int main(){
    
    struct Node* head = createNode(0);
    struct Node* tail = createNode(0);
    
    head -> next = tail;
    tail -> next = head;
    
    enqueue(5,tail);
    dequeue(head);

    display(head,tail);
}
```
### application of stacks
#### infix
the general math notation where the operator is written in-between the notations
#### prefix
the operator is placed before the operands 
#### postfix
the operator is placed after the operands

***
## tree
#### binary tree
binary tree is a type of tree data structure where each node can have maximum two children nodes.

1. full binary tree
	1. considered to have only 0 or 2 children 
2. complete binary tree
	1. all nodes are filled completely except the last level. 
	2. All the nodes must be to the left as much as possible
3. perfect binary tree
	1. if all nodes have 2 children 
	2. all the leaf nodes are at the same level
4. degenerated binary tree
	1. all internal nodes have one children 
5. balanced binary tree 
	1. left and right binary tree differ by 1

### threaded binary tree
in a threaded binary tree, either of the pointer node of the leaf node is made to point to their parent.

*a threaded binary tree is needed when space usage constraints exist*

## types of binary traversal

## inorder
![[DSA_1.webp]]
## preorder
![[DSA_2.webp]]
## postorder
![[DSA_3.webp]]
#### types
- single threaded
- double threaded
# N-ary tree
- full n-ary tree
- complete n-ary tree
- perfect n-ary tree

***
# Module 3
### trees
- trees is a collection of nodes connected by edges
- types,
	- linear
	- non-linear - a node is connected to more than one nodes
- terminologies 
	1. root
		the top node in a tree
		![[DSA_1.png]]
	2. child
		a node directly connected to another node when moving away from the root
		![[DSA_2.png]]
	3. parent
		the node under which child nodes are connected
	4. siblings
		group of nodes with the same parent
		![[DSA_3.png]]
	5. descendant
		a node reachable by repeatedly moving from parent and child
		![[DSA_4.png]]
	6. ancestor
		a node reachable by repeatedly moving from child to parent
		![[DSA_5.png]]
	7. leaf
		a node with no children
		![[DSA_6.png]]
	8. degree
		the number of subtrees of a node
		![[DSA_7.png]]
	9. edge
		connection between one node and another
		![[DSA_8.png]]
	10. height of node
		the number of edges on the longest path between the node and a leaf
		![[DSA_9.png]]
	11. height of tree
		its the heigh of the root node
		![[DSA_10.png]]
	12. depth
		it is the number of edges from that node to its tree root
		![[DSA_11.png]]
### binary tree
- binary tree is a tree data structure in which each node has at most two children which are referred to left child and right child.
- types
	- perfect or full binary tree
		all interior nodes have two children and all leaves are at the same depth
		![[DSA_12.png]]
	- complete binary tree
		left subtree must be completely filled but right subtree may or may not be filled
		![[DSA_13.png]]
	- ordered or binary search trees
		![[DSA_14.png]]
		smaller values are inserted to the left of the node, and larger values are inserted to the right subtree
#### tree traversal
- the process of checking or updating each node in tree data structure exactly once
- types,
	- pre-order
		- print the data 
		- traverse to left sub-tree 
		- traverse right subtree
		![[DSA_15.png]]
		ans: 20,8,4,12,10,14,22

		```c
		void preOrder(treePointer ptr){
			if(ptr != NULL){
				visit(ptr);
				preOrder(ptr -> left);
				preOrder(ptr -> right);
			}
		}
		```

	- in-order
		- traverse the left sub-tree 
		- print the data 
		- traverse right subtree
		![[DSA_15.png]]
		ans: 4,8,10,12,14,20,22
		
	```c
	void inOrder(treePointer ptr){
		if(ptr != NULL){
			inOrder(ptr -> left);
			visit(ptr);
			inOrder(ptr -> right);
		}
	}
	```
	- post-order
		- traverse the left sub-tree 
		- traverse the right sub-tree 
		- print the data
		![[DSA_15.png]]
		ans: 4, 10, 14, 12, 8, 22, 20
		
	```c
	void postOrder(treePointer ptr){
		if(ptr != NULL){
			postOrder(ptr -> left);
			postOrder(ptr -> right);
			visit(ptr);
		}
	}
	```
	- level order
		just print the nodes of the same level as you descend 
		![[DSA_15.png]]
		ans: 20, 8, 22,4,12, 10, 14

### Binary heaps
- a binary heap is a complete binary tree
#### heap order property
- heap order property states that every child node must be either greater or lesser than its parent node depending on the heap type.
	![[DSA_16.png]]
	this is not a heap as 20 has a child node of value 15

- A max tree is a tree in which the parent node is greater than its child nodes. When a max tree is a complete binary tree, its called Max heap
	![[DSA_18.png]]
- a min tree is a tree in which the parent node is lesser than its child nodes. When a min tree is a complete binary tree, its called Min heap.
	 ![[DSA_19.png]]
### data structures
- unordered linked list
- unordered arrays
- sorted linked list
- sorted arrays
- heaps
### priority queue representation

| Representation        | Insertion | deletion |
| --------------------- | --------- | -------- |
| Unordered linked list | O(1)      | O(n)     |
| Unordered arrays      | O(1)      | O(n)     |
| Sorted linked list    | O(n)      | O(1)     |
| Sorted arrays         | O(n)      | O(1)     |
| Max heap<br>          | O(logn)   | O(logn)  |
## AVL trees

an AVL trees is a binary search tree in which for every node, the difference between the heights of its left and right subtrees, called the balance factor, is at most 1.
![[DSA_20.png]]
(a) is an AVL tree while (b) is not an AVL tree, as the balance factor of the root node is more than 1.

### avl tree rotations
if a key insertion violates the balancing requirement at some point, then the subtree node is rotated via one of the four transformations
1. L rotation
	![[DSA_23.png]]
2. R rotation 
	![[DSA_1.jpg]]
1. LR rotation
	![[DSA_2.jpg]]
1. RL rotation
	![[DSA_3.jpg]]

- search, insertion, and deletion are O(logn)
- its disadvantages are frequent rotations and high complexity
***
# Module 5
## hashing
- useful of quickly storing and retrieving data
- useful for performing optimal searches 
- the reason we use hashes instead of trees is because hashing provides the same insertion, deletion, and search functionalities in O(1) time rather than O(logn) time by trees.
## hashing table
- hash table is a data structure that stores data in associative manner
- each data has its own unique index number. If we know its index then we can retrieve the data quickly
- common hash ADTs are
	1. CreateHashTable
	2. HashSearch
	3. HashInsert
	4. HashDelete
	5. DeleteHashTable
$$\implies Key\\\ \%\\\ Table\ size $$
- implementation of hash table is called hashing
- Key is the data that needs to be stored in the hash table, so hash function converts the key to its address.
- A good hash function should,
	1. minimize collision
	2. be easy and quick to compute
	3. distribute the keys evenly
	4. use all the information from the key
	5. have a high load factor for a given set of keys
		- load factor is the number of elements stored in the hash table divided by its size. it says how evenly the function is distributing the keys and thus determining the function's efficiency.
## collisions
- hash functions are used to map each key to a different address space
- but practically no hash function can be fully collision free, so there are techniques to resolve
- collision is a condition that occurs when two records are stored in the same address space
## collisions resolution techniques
- the process of finding an alternate location is called collision resolution technique
- hash tables are more efficient than trees in managing collisions
- popular types are
	1. Direct chaining
		- when two or more keys are hashed to the same location, they are constituted into a singly linked list called a chain
		- this is also called open hashing or separate chaining
	2. open addressing
		- all the keys are stored in the hash table itself and collisions are resolved by probing
		- this is also called closed hashing
		- types of probing,
			1. Linear probing
				- the interval between each element is 1 
				- if the current place is occupied the algorithm checks for the next place. 
				- If it is free then the key is placed there, if not then the next place is checked.
				- $rehash(key) = (n+i)\ \%\ tablesize$
			2. Quadratic probing
				- this method avoids clustering of data faced in linear probing
				- $rehash(key) = (n+i^2)\ \%\ tablesize$
			3. Double hashing
				- double hashing uses two hashing functions

***
## searching

-  searching is the process of finding an item with specified properties from a collection of items
- sorting is used to aid the searching algorithms making it more efficient
### types of searching
- unordered linear search
	- search an entire list of elements
	- space complexity is O(1) and time complexity is O(n)
- ordered linear search
	 - if the searched value is greater than the data to be searched, then the algorithm returns -1
	 - else the data is found and is returned.
- binary search
	 - requires a sorted list
	 - follows divide and conquer method where the list is divided into two halves and the middle element is always compared 
	 - if match is found then the middle value index is returned
	 - if not, we search into either halves based on where the data might be present
	 - best case - O(n), average and worst case - O(logn)
- interpolation search
- binary search tree
- symbol tables and hashing
	 - symbol table associates its data with a key, so it is quick and easy for retrieval.
- string searching algorithms
## sorting
- sorting is an algorithm that arranges the elements of the list in a certain order, either ascending or descending 
- sorting is necessary as it can reduce the time complexity of searching algorithms significantly
- main factors for testing the sorting algorithm's efficiency,
	1. number of comparison
	2. number of swaps
	3. memory usages
	4. recursion
	5. stability 
	6. adaptability
- classification based on the type of memory used,
	1. internal sort - that uses high speed internal memory during classification
	2. external sort - that uses external memory 
### classification based on comparisons
#### comparison based
##### 1. bubble sort
- simplest sorting algorithm
- works by iterating through the input array and swapping each pair of elements if it's required
- insertion sort is better than bubble sort
- high time complexity is a disadvantage
- best case -> O(n), worst case and average case -> O(n<sup>2</sup>)

```c
void bubbleSort(int A[], int n){
	int temp;
	for(int end = n-1; n >= 0; n--){
		for(int start = 0; start <= end-1; start++){
			if(A[i] > A[i+1]){
				temp = A[i];
				A[i] = A[i+1];
				A[i+1] = temp;
			}
		}
	}
}
```
##### 2. selection sort
- its in in-place sorting algorithm
- it works well for small keys with large values
- the algorithm works by finding the minimum value in the list and swapping it with the current value
- this algorithm is called selection sort since it repeatedly selects the small element
- best case, worst case, average case -> O(n<sup>2</sup>)

```c
void selectionSort(int A[], int n){
	int min, temp;
	for(int i = 0; i < n-1; i++){
		min = i;
		for(int j = i+1; j < n; j++){
			if(A[min] > A[j]){
				min = j;
			}
		}
		temp = A[min];
		A[min] = A[i];
		A[i] = A[min];
	}
}
```
##### 3. insertion sort
- insertion sort is simple and efficient sort where in each iteration, an element is removed from the input data and is placed in correct position of a sorted list
- the choice of element being removed is random and this process is repeated until all the elements are covered
- this is efficient for small data
- practically more efficient than selection and bubble sort, even though they all have O(n<sup>2</sup>)
- best case -> O(n) and average and worst case is O(n<sup>2</sup>)

```c
void insertionSort(int A[], int n){
	int key,j;
	for(int i = 0; i < n; i++){
		key = A[i];
		j = i-1;
		while(j >= 0 && A[j] > key){
			A[j+1] = A[j];
			j--;
		}
		A[j+1] = key;
	}
}
```
##### 4. merge sort
- merge sort is an example of divide and conquer strategy
- merging is the process of combining two sorted files into a bigger sorted file
- selection is the process of dividing a file into two parts
- best, average, worst case -> O(nlogn)
##### 5. heap sort
- heap sort is a comparison based sorting algorithm and is part of the selection sort family
- heap sort is an in-place sort but it is not a stable sort
- best, average, worst case -> O(nlogn)

```c
void heapSort(int A[]){
	int heapSize = n;
	build_maxHeap(A);
	for(int i = n; i >= 2; i--){
		swap(A[1],A[i]);
		heapSize--;
		max_heapify(A,1,heapSize);
	}
}
```
##### 6. quick sort
- quick sort is an in-place sorting algorithm which means it doesn't take any additional space
- it uses the same algorithm to sort the elements
- it uses the divide and conquer method
- it divides the large arrays into smaller arrays
- Partitioning : The algorithm picks a pivot and arranges the elements in such a way that all the elements that are lesser than the pivot should be on the left side and larger values to the right
- at the end of the operation the pivot element will be placed at its sorted position

##### 7. shell sort
- invented by donald shell
- it is an generalization of insertion sort
- instead of only comparing the adjacent elements like in insertion sort, shell sort makes several passes

##### 8. tree sort
- tree sort uses binary search tree. It involves scanning each element and placing it into the proper position in a binary search tree
- tree sort has two phases
	- first is creating a binary search tree using the given inputs
	- second is traversing the tree using in-order traversal to give a sorted array

| Name          | average case     | worst case               |
| ------------- | ---------------- | ------------------------ |
| bubble        | O(n<sup>2</sup>) | O(n<sup>2</sup>)<br>     |
| selection     | O(n<sup>2</sup>) | O(n<sup>2</sup>)<br>     |
| insertion     | O(n<sup>2</sup>) | O(n<sup>2</sup>)<br>     |
| shell         | -                | O(nlog<sup>2</sup>n)<br> |
| merge sort    | O(nlogn)         | O(nlogn)                 |
| heap sort     | O(nlogn)         | O(nlogn)                 |
| quick sort    | O(nlogn)         | O(n<sup>2</sup>)         |
| tree sort<br> | O(nlogn)         | O(n<sup>2</sup>)         |
