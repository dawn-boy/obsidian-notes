# Fast-slow pointer technique
Also called as Tortoise-Hare technique where 
- A Slow pointer moves linearly
- A Fast pointer moves twice as fast as the slow one
### Intuition
The idea here is if the fast pointer moves twice as fast then by the time it reaches the end, The slower one would be in the middle.
### Code
```c++
Node* slow = head;
Node* fast = head;

while (fast != nullptr && fast->next != nullptr) {
    slow = slow->next;
    fast = fast->next->next;
}
```
##### ==Note==
Always check head for `nullptr` before proceeding to avoid `Segmentation Error`.

```c++
if(head == nullptr) return;
```

This technique is mainly used in Linked lists for solving problems at `O(1)` time in `O(n)` space complexity.

## Floyd's Algorithm
If the list is cyclic, then eventually the fast pointer would meet the slow pointer.

```c++
bool hasCycle(Node* head) {
    Node* slow = head;
    Node* fast = head;

    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;
        if (slow == fast)
            return true;
    }
    return false;
}
```

The point where they meet is the starting point of the cycle.

***
## Binary to Decimal
To understand this we must grasp the beautiful structure of mathematics. 

> “When the answer aligns with mathematical invariants, the answer is often a simple equation…”

without having to involve other data structures or loops within loops, etc.

#### Decimal sense
In decimal sense, the value of each digit is given by
$$\implies N * b + x$$
where, $N \rightarrow already\ existing\ number$
$b \rightarrow base$
$x \rightarrow right\ most\ digit$

i) Let's say,
$$x = 0$$
then we can express that by
$$0 * 10 + 0 \implies 0$$

ii) If i append 5 right-hand side
$$ x= 05 \implies 5$$
mathematically what happened is,
$$0 * 10 + 5 \implies 5$$

iii) Append 6 again,
$$x = 56$$
$$5 * 10 + 6 \implies 56$$
iv) Append 4 again,
$$x = 564$$
$$56*10 + 4 \implies 564$$

### Why this works?
Well, what can I say, math operates harmoniously 

this works only because,
$$56*10 + 4 \implies 564$$

it translates to this,
$$(5*10 + 6) * 10 + 4 \implies 564$$
which again says,
$$((0*10 + 5) * 10 + 6) * 10 + 4$$
What you're witnessing now is the true glorious self of the number `564`. 
Look how the `10` that's multiplied later propagates itself leftwards, and that's the mathematical translation of the literal saying 

> Appending a digit on the right increases the place value of all digits to its left.

even if you append a $0$, the base $10$ propagates,
$$x = 1$$
so, $0*10 + 1 \implies 1$
and appending a $0$ would mean,
$$\implies 1 * 10 + 0$$
$$(0*10 + 1) * 10 + 0$$
$$\implies (0 * 10^2 + 10 )+ 0 \implies (0 + 10) + 0$$
$$= 10$$
Did you see how the propagated base $10$ got itself multiplied with its MSB digit bases and increased the value relatively to its LSB digits?

This is hearing the music of math.

### Binary sense
$$\implies N * b + x$$
The same thing except base is not $10$ but $2$.
$$\implies N * 2 + x$$
## Code
We've a linked list where each node represents a binary digit (0 or 1). The goal of the `binaryToDecimal` function is to convert this binary number, represented by the linked list, into its decimal equivalent.
```c++
int binaryToDecimal(){
	if(head == nullptr) return 0;
	
	Node* current = head;
	int num = 0;
	
	while(current != nullptr){
		num = num * 2 + current->value;
		current = current->next;
	}
	return num;
}
```

***
## Linked list partitioning

> Partitioning is classification, not re-arrangement. We classify them once and then concatenate into a bigger list.
## **Rearrange the list so that all nodes with value `< x`  occurs in first half and nodes with value `>= x` occurs in second half of the list**

### Core Idea
We create two logical *(its purely logical because in algorithmic sense we just re-used the same list by shuffling the pointers.)* sublists
- one for values `< x`
- one for values `>= x`

We're not
- creating new nodes,
- Not gonna allocate extra memory
We're just changing the `next` pointers.

==So, space stays O(1)==

### Thought process
1. Walk the list once
	- every node is visited exactly once -> O(n) time complexity

2. Detach the current node
```c++
	Node* rest = curr->next;
	curr->next = nullptr;
```
- This is important because 
	- each node becomes a clean standalone unit
	- which can be safely attached elsewhere
	- it prevents accidental loops

3. Classify the node
	- if `value < x` -> goes to `less` list
	- else -> goes to `large` list

4. Append in O(1)
	- each logical sublist maintains a `head` and `tail`
	- appending is constant time

5. Move forward
```c++
	curr = rest;
```

Finally we merge,
```c++
head = largeHead;

lessTail->next = largeHead;
head = lessHead;
tail = largeTail;
```
***
### Reversing elements between a given indices

```c++
    void reverseBetween(int m, int n){
        if (head == nullptr) return;

        Node* dummy = new Node(0);
        dummy->next = head;
        Node* prev = dummy;

        for(int i = 0; i<m; i++) prev = prev->next;

        Node* current = prev->next;
        for(int i = 0; i<n-m; i++){
            Node* temp = current->next;
            current->next = temp->next;
            temp->next = prev->next;
            prev->next = temp;
        }

        head = dummy->next;
        delete dummy;
    }
```

