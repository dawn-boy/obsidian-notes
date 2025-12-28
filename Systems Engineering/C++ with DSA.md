## Struct definition
```c++
#include <iostream>
#include <string>

struct Location{
    int id;
    std::string name;
    int x;
    int y;
};

int main(){

    Location myHome;
    Location dest;

    myHome.id = 1;
    myHome.name = "Home";
    myHome.x = 20;
    myHome.y = 21;

    dest.id = 2;
    dest.name = "Destination";
    dest.x = 50;
    dest.y = 100;

    std::cout << myHome.id << " " << myHome.name << " " << "(" << myHome.x << "," << myHome.y << ")";
    std::cout << std::endl;
    std::cout << dest.id << " " << dest.name << " " << "(" << dest.x << "," << dest.y << ")";
    std::cout << std::endl;

    return 0;
}
```

# 1. Vector (The Dynamic Array)
- A regular array, the number of elements that can be store is fixed at declaration. 
- But a `vector` expands its size as new items are being added!
#### Why use a Vector?
- **Contiguous Memory:** All items sit right next to each other in your RAM. This makes it incredibly fast for the computer to read.
- **Automatic Growth:** You don't have to worry about the size; you just `push_back` data.

## Example code
```c++
#include <iostream>
#include <string>
#include <vector>

struct Location{
    int id;
    std::string name;
    int x;
    int y;
};

int main(){

    Location myHome;
    Location dest;

    myHome.id = 1;
    myHome.name = "Home";
    myHome.x = 20;
    myHome.y = 21;

    dest.id = 2;
    dest.name = "Destination";
    dest.x = 50;
    dest.y = 100;

    std::vector<Location> universe;
    universe.push_back(myHome);
    universe.push_back(dest);

    for(int i = 0; i<universe.size(); i++){
        std::cout << universe[i].id << " " << universe[i].name  << " " << universe[i].x  << " " << universe[i].y  << " " << std::endl;
    }

    return 0;
}
```

## Why `vector` can be powerful yet **EXPENSIVE**?
When you `push_back` an item into a vector, the computer doesn't just find a random spot for it. It needs all items to be side-by-side in memory (this is called Contiguous Memory).

**Here is the problem**: What if the computer runs out of room right next to your current list?
- It allocates a new, larger chunk of memory somewhere else.
- It copies all your old items to the new spot.
- It deletes the old memory.
This is called **Reallocation**, and it's why Vectors are powerful but can be *expensive* if you do it too often.
## Pointers
Everything has an address in C++. A pointer is just a variable that stores that address.

- `int a = 10;` — Stores the value 10.
- `int* p = &a;` — The `*` means "this is a pointer." The `&` means "get the address of."

When using a pointer, we use `->` instead of `.` to access the struct attributes.

```c++
    Location* homePtr = &myHome;
    Location* destPtr = &dest;

    std::cout << homePtr << std::endl;
    std::cout << destPtr << std::endl;
    std::cout << destPtr->name << std::endl;
```
***
## Build `std::vector`
Since we have to manage our memory manually. we have to use `new` and `delete` keywords.

We need,
1. **A Pointer**: to start our data block in RAM.
2. **Size**: to know how much items it currently occupies.
3. **Capacity**: to know when to resize.

## The Idea
```c++
class DynamicArray{
private:
	// Attribute variables
	
public:
	constructor(){
		// initializing attributes
	}	

	~destructor(){
		// clearing out the data
	}
	
	void push_back(){
		if(size == capacity){
			resize();
		}
		// adding logic
	}
	
	void resize(){
		// Double the capacity
		
		// assign a new memory location
		// copy the old data to new memory location
		
		// delete the old array
		
		// point the data var to new arry
	}
	
	void printAll(){
		// print all the data
	}
}
```

## The code
```c++
#include <iostream>
#include <string>

struct Location{
    int x;
    int y;
    std::string name;
    int id;
};

template <typename T>
class DynamicArray{
private:
    T* data;
    int index;
    int size;

public:
    DynamicArray(){
        size = 2;
        index = 0;
        data = new T[size];
    }
    ~DynamicArray(){
        delete[] data;
    }
    void push_back(const T loc){
        if(index == size) resize();

        data[index] = loc;
        index++;
    }
    void show() const {
        for(int i = 0; i < size; i++) std::cout << data[i].name << " ";
        std::cout << std::endl;
    }
    void resize(){
        std::cout << "Extending from " << size << " to " << size*2 << std::endl;
        size *= 2;
        T* newData = new T[size];

        for(int i = 0; i < index; i++) newData[i] = data[i];

        delete[] data;
        data = newData;
    }
};


int main(){

    Location myHome;
    myHome.x = 20;
    myHome.y = 30;
    myHome.id = 1;
    myHome.name = "Home";

    Location dest;
    dest.x = 50;
    dest.y = 50;
    dest.id = 2;
    dest.name = "Destination";

    DynamicArray<Location> map;

    map.push_back(myHome);
    map.show();
    map.push_back(dest);
    map.show();
    map.push_back(myHome);
    map.show();
    map.push_back(myHome);
    map.show();
    map.push_back(myHome);
    map.show();
    map.push_back(dest);
    map.show();
    map.push_back(dest);
    map.show();
    map.push_back(dest);
    map.show();

    return 0;
}
```

- we have used Generic programming concepts `template <typename T>` to adapt to any datatype given in `main`
### Output
```c++
Home  
Home Destination 
Extending from 2 to 4
Home Destination Home  
Home Destination Home Home 
Extending from 4 to 8
Home Destination Home Home Home    
Home Destination Home Home Home Destination   
Home Destination Home Home Home Destination Destination  
Home Destination Home Home Home Destination Destination Destination 
```
### Bench-marking the code
```c++
int main(){
    const int totalItems = 1000000;
    DynamicArray<int> myArr;
    std::vector<int> stdVec;

    auto start1 = std::chrono::high_resolution_clock::now();
    for(int i = 0; i<totalItems; i++) myArr.push_back(i+1);
    auto end1 = std::chrono::high_resolution_clock::now();

    std::chrono::duration<double> elapsed_time_dyn = end1-start1;

    auto start2 = std::chrono::high_resolution_clock::now();
    for(int i = 0; i<totalItems; i++) stdVec.push_back(i+1);
    auto end2 = std::chrono::high_resolution_clock::now();

    std::chrono::duration<double> elapsed_time_vec = end2-start2;

    std::cout << "My Dynamic Array took: " << elapsed_time_dyn.count() << std::endl;
    std::cout << "STL vector took: " << elapsed_time_vec.count() << std::endl;
}
```

### Output
```c++
My Dynamic Array took: 0.00676549
STL vector took: 0.0213556
```

==Our performed better because `std::vector` implements a lot of safety checks that my `DynamicArray` ignores.==

***
# 2. Linked Lists
- We learnt that Dynamic arrays are contiguous in memory, meaning they are storing one after another. But ==**Linked lists are polar opposites**==
In a Linked List, All the items are scattered throughout the main memory.
Each Item (node) has two parts:
- The Data: The data itself
- The Pointer: A link to where the next item is hidden
### Why even use LinkedLists if vectors are fast?
 Instant Insertion
	If you want to insert a new element in the middle of 1 million items vector. You have to slide every element over to make room.
### Singly linked lists Code
```c++
#include <iostream>

template <typename T>
struct Node{
    T data;
    Node* next;
};

template <typename T>
class LinkedList{
private:
    Node<T>* head;
public:
    LinkedList(){
        head = nullptr;
    }

    void push_front(const T value){
        Node<T>* node = new Node<T>{value, nullptr};
        node->next = head;
        head = node;
    }

    void push_back(const T value){
        Node<T>* node = new Node<T>{value, nullptr};

        if(head == nullptr) {
            head->next = node;
            return;
        }

        Node<T>* temp = head;
        while(temp->next != nullptr) temp = temp->next;
        temp->next = node;
    }
    void push_middle(const T value, const T addAfter){
        Node<T>* temp = head;
        while(temp->next != nullptr){
            if(temp->data == addAfter){
                Node<T>* newNode = new Node<T>{value, temp->next};
                temp->next = newNode;
                return;
            }
            temp = temp->next;
        }
    }
    void remove(const T value){
        // 1. The Whole list is empty
        if(head == nullptr) return;

        // 2. the node to delete is HEAD
        if(head->data == value){
            Node<T>* temp = head;
            head = head->next;
            delete temp;
            return;
        }

        // 3. searching for the node 
        Node<T>* current = head;
        Node<T>* prev = nullptr;
        while(current != nullptr && current->data != value){
            prev = current;
            current = current->next;
        }


        // if nothing is found
        if(current == nullptr) {
            std::cout << "Element " << value << " was not found in the linked List." << std::endl;
            return;
        }

        // if found
        prev->next = current->next;
        delete current;
    }

    void show() const {
        Node<T>* temp;
        temp = head;
        while(temp != nullptr){
            std::cout << temp->data << ", " << temp->next << std::endl;
            temp = temp->next;
        }
    }
};

int main(){

    LinkedList<int> list;
    list.push_front(40);
    list.push_front(80);
    list.push_back(400);
    list.push_middle(34,40);
    list.remove(40);
    list.show();

    return 0;
}
```

