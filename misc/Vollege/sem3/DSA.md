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
## backtracking

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

void insert(int data, struct Node* temp){
    struct Node* ref = temp -> next;
    temp -> next = createNode(data);
    temp -> next -> next = ref;
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
```c
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

***
## tree
#### binary tree
binary tree is a type of tree data structure where each node can have maximum two children nodes.

1. full binary tree
	1. considered to have only 0 or 2 children 
2. complete binary tree
	1. all nodes are filled completely except the last level 
3. perfect binary tree
	1. if all nodes have 2 children 
4. degenerated binary tree
	1. all internal nodes have one children 
5. balanced binary tree 
	1. left and right binary tree differ by 1

