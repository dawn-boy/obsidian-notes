## 1. Variables and datatypes
```c++
datatype variable_name = value;
int age = 20;
float price = 99.5;
char grade = 'A';
bool isPass = true;
```
***
## 2. Input and output
- `cin` -> input
- `cout` -> output

```c++
#include <iostream>
using namespace std;

int main() {
    int age;
    cout << "Enter your age: ";
    cin >> age;
    cout << "Your age is " << age << endl;
    return 0;
}
```
***
## 3. Conditionals
1. `if` / `else if` / `else`
```c++
if (x > 0) {
    cout << "Positive";
} else if (x < 0) {
    cout << "Negative";
} else {
    cout << "Zero";
}
```

2. ternary operator
```c++
string result = (x % 2 == 0) ? "Even" : "Odd";
```
***
## 4. Loops
1. `for` loop
```c++
for (int i = 0; i > 10; i--) {
    cout << i << " ";
}
```

2. multiple variables `for` loop
```c++
for (int i = 1, j = 10; i <= j; i++, j--) {
    cout << i << " " << j << endl;
}
```

3.  `break` and `continue`
```c++
for (int i = 1; i <= 10; i++) {
    if (i == 5) continue; // skip
    if (i == 9) break;    // stop
    cout << i << " ";
}
```

4. infinite loop
```c++
for (;;) {
    // runs forever
}
```

5. Nested loop
```c++
for (int row = 1; row <= R; row++) {
    for (int col = 1; col <= C; col++) {
        cout << "*";
    }
    cout << endl;
}
```
### Loop based star generation
```c++
#include <bits/stdc++.h>
using namespace std;

int main(){
	int rows = 4;
	for(int row = 1; row<=rows; row++){
		for(int spaces = 1; spaces<=rows-row; spaces++) cout << " ";
		for(int stars = 1; stars<=2*row-1; stars++) cout << "*";
		cout << endl;
	}
	for(int row = rows-1; row>=1; row--){
		for(int spaces = 1; spaces<=rows-row; spaces++) cout << " ";
		for(int stars = 1; stars<=2*row-1; stars++) cout << "*";
		cout << endl;
	}
}
```
***
## 5. Functions
#### syntax
```c++
return_type functionName(dataytype parameter) {
    // ...
    return value;
}
```

#### Declaration (prototype)
```c++
int sum(int, int);
```
#### Definition
```c++
int sum(int a, int b) { return a + b; }
```

#### Pass by value and Pass by reference
```c++
// pass by value (copy)
void fun(int x) {
    x = 10; // original not changed
}

// pass by reference (original)
void fun(int &x) {
    x = 10; // original changed
}
```

Use reference when
- you want to change the original value
- avoid copying large data

#### Default arguments
```c++
int add(int a, int b = 5) {
    return a + b;
}

add(10);    // 15
add(10, 2); // 12
```

#### Inline functions
```c++
inline int cube(int x) { return x*x*x; }
```
- compiler expands the functions directly
- faster for smaller body functions

## Recursion
its a function calling itself
- Base Case → stops recursion
- Recursive Case → continues recursion
#### example
```c++
int fact(int n) {
    if (n == 0) return 1; // base case
    return n * fact(n - 1); // recursive case
}
```
#### when to use recursion
- Problems based on repeated substructures (trees, graphs)
- Backtracking (maze, sudoku)
- Divide and conquer (merge sort, quicksort)
***
## 6. Array
A collection of elements of the same datatype, stored in contiguous memory.
```c++
// declaration
int arr[5] = {10, 20, 30, 40, 50};

// accessing
arr[0];   // first element
arr[n-1]; // last element
```

- uses fixed size
- elements are stored in a contiguous manner
- elements accessed in O(1) time using index

### Linear search
```c++
int search(int arr[], int n, int key) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == key)
            return i; // index
    }
    return -1; // not found
}
```
##### Time Complexity:
- Best: O(1)
- Worst: O(n)
### Binary search
```c++
int binarySearch(int arr[], int n, int key) {
    int l = 0, r = n - 1;

    while (l <= r) {
        int mid = (l + r) / 2;

        if (arr[mid] == key) return mid;
        else if (arr[mid] < key) l = mid + 1;
        else r = mid - 1;
    }
    return -1;
}
```
##### Complexity:
- O(log n)
***
## 2D arrays
```c++
datatype arr[rows][cols];
int mat[3][3] = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```

##### Memory layout
- 2D arrays are stored row-wise in contiguous memory
```c++
int arr[3][4];
```

in-memory:
```
Row 0: [a00 a01 a02 a03]
Row 1: [a10 a11 a12 a13]
Row 2: [a20 a21 a22 a23]
```
***
## 7. Strings
```c++
string s;
cin >> s;        // stops at space

// to get in a full line
getline(cin, s);
```

String Size & Access
```c++
string s = "paradox";

s.size();     // length
s.length();   // same as size()
s[0];         // first char
s.back();     // last char
s.front();    // first char
```

Modify
```c++
// append
s += "xyz";
s.append("abc");

// push and pop
s.push_back('a');
s.pop_back();

// insert
s.insert(3, "HELLO");

// erase
s.erase(2, 3);   // start=2, erase 3 chars

// replace
s.replace(1, 2, "XX");

// substring
string sub = s.substr(2, 4);  
// start=2, length=4
```

Search
```c++
// find substring
s.find("lo");

// find from end
s.rfind("lo");

// find character
s.find('a');
```

Comparision
```c++
if (s1 == s2) {}
if (s1 < s2) {}    // lexicographic comparison
```

Conversion
```c++
// string to int, long long
int x = stoi(s);
long long y = stoll(s);

// to string
string s = to_string(x);
```
***
# 8. Strings
## 1. Creation & Input
```c++
string s = "hello";
cin >> s;          // stops at spaces
getline(cin, s);   // full line input
```

## 2. Length & Size
```c++
s.length()
s.size()
```
Both return number of characters.
## 3. Accessing Characters
```c++
s[i];         // indexing
s.front();    // first char
s.back();     // last char
```

## 4. Modify Strings
### Append
```c++
s += "abc";
s.append("xyz");
```
### Insert
```c++
s.insert(pos, "HELLO");
```
### Erase
```c++
s.erase(pos, count);
```
### Replace
```c++
s.replace(pos, count, "NEW");
```
### Push/Pop
```c++
s.push_back('a');
s.pop_back();
```

## 5. Substrings
```c++
s.substr(start, length);
```
Example:
```c++
string part = s.substr(2, 5);
```

## 6. Searching
### Find substring
```c++
s.find("abc");
```
### Find char
```c++
s.find('a');
```
### Reverse find (from end)
```c++
s.rfind("abc");
```
Returns index OR `string::npos` if not found.

## 7. Comparison
```c++
s1 == s2
s1 != s2
s1 < s2      // lexicographic
s1 > s2
```
## 8. Conversion
### String → Int
```c++
stoi(s)
stoll(s)
stof(s)
stod(s)
```
### Int → String
```c++
to_string(x);
```

### Most Used String Algorithms 
#### A. Count characters
```c++
for(char c : s) { count++ }
```
#### B. Reverse string
```c++
reverse(s.begin(), s.end());
```
#### C. Check palindrome
```c++
bool isPalindrome(string s) {
    int i = 0, j = s.size() - 1;
    while(i < j)
        if(s[i++] != s[j--]) return false;
    return true;
}
```
#### D. Count vowels
```c++
int count = 0;
for(char c : s) {
    c = tolower(c);
    if(c=='a'||c=='e'||c=='i'||c=='o'||c=='u')
        count++;
}
```
#### E. Remove spaces
```c++
string s;
string r;
for(char c : s)
    if(c != ' ') r += c;
```
#### F. Uppercase / Lowercase
```c++
for(char &c : s) c = toupper(c);
for(char &c : s) c = tolower(c);
```
#### G. Frequency array (a–z)
(critical for anagrams, hashing, string problems)
```c++
int freq[26] = {0};
for(char c : s)
    freq[c - 'a']++;
```
***
# 9. Pointers
## **1. What is a Pointer?**
A **pointer** is a variable that stores the **memory address** of another variable.
```c++
int a = 10;
int* p = &a;
```
- `a` → stores **value**
- `p` → stores **address** of `a`
- `&a` → address-of operator
- `*p` → dereference operator (gives the value stored at that address)
## **2. Address-of Operator (`&`)**
Used to get the **memory address** of a variable.
```c++
int x = 5;
cout << &x;
```
Outputs a hexadecimal address like `0x7ffeefbff45c`.
## **3. Dereference Operator (`*`)**
Used to **access the value stored at an address**.
```c++
int x = 5;
int* p = &x;
cout << *p;   // prints 5
```
You can also **modify** through pointer:
```c++
*p = 20;   // x becomes 20
```
## **4. Declaring Pointers**
```c++
int* p;   // pointer to int
char* c;  // pointer to char
float* f; // pointer to float
```
Pointer **size is always the same** (8 bytes on 64-bit systems), regardless of data type.
## **5. Uninitialized & Wild Pointers**
BAD:
```c++
int* p;     // uninitialized → points anywhere
*p = 10;    // dangerous!
```
Always initialize:
```c++
int* p = nullptr;
```
## **6. Null Pointer**
A pointer that points to **nothing**.
```c++
int* p = nullptr;
```
You must always check before dereferencing:
```c++
if (p != nullptr) {
    cout << *p;
}
```
## **7. Pointer to Pointer**
A pointer that stores address of a pointer.
```c++
int x = 10;
int* p = &x;
int** pp = &p;
```
Meaning:
- `pp` → address of `p`
- `*pp` → same as `p`
- `**pp` → same as `x`
## **8. Memory Layout Basics**
Two main memory areas:
### **Stack**
- Used for normal variables
- Auto-managed
- Fast
### **Heap**
- Used for dynamic memory (`new`, `delete`)
- You manually manage size
- Slower, but flexible
Pointers are used to access heap memory (will be Day 10).
## **9. Common Pointer Mistakes**
- Using uninitialized pointer  
- Dereferencing null pointer  
- Memory leaks (Day 10)  
- Dangling pointers:
Example:
```c++
int* p = new int(10);
delete p;
cout << *p;  // DANGEROUS
```

## Problems
1. Reverse an array using pointers
```c++
#include <bits/stdc++.h>
using namespace std;

void display(int* arr, int n){
    for(int i = 0; i < n; i++) cout << arr[i] << " ";
    cout << endl;
}

void swap(int* ptr1, int* ptr2){
    int temp;

    temp = *ptr2;
    *ptr2 = *ptr1;
    *ptr1 = temp;
}

void reverser(int n, int arr[]){
    int* front = arr;
    int* back = arr+n-1;
    
    while(front < back) {
        swap(front, back);
        front++;
        back--;
    }
}

int main(){
    int size = 5;
    int arr[size] = {3,4,5,6,7};
    cout << "Before reversing: ";
    display(arr, size);
    reverser(5, arr);
    cout << "After reversing : ";
    display(arr, size);
    return 0;
}
```

2. write a `strlen()` function to count the length of given string
```c++
#include <bits/stdc++.h>
using namespace std;

int strlen(char* str){
	int count = 0;
	while(*str != '\0'){
		count++;
		str++;
	}
	return count;
}
int main(){
	char str[] = "Adhi";
	cout << "The length of (" << str << ") is " << strlen(str);
}
```

3. Add using pointer for result location
```c++
#include <bits/stdc++.h>
using namespace std;

int addP(int* result, int a, int b){
    if(result != nullptr){
        *result = a+b;
        return 0;
    }
    return -1;
}

int main(){
    int a = 4;
    int b = 10;
    int c = 0;
    int *result = &c;
	
    cout << "Before: " << *result;
    cout << endl;
    addP(result, a, b);
	
    cout << "After: " << *result;
    cout << endl;
	
    return 0;
}
```

4. Check if a pointer is insider the given array
```c++
#include <bits/stdc++.h>
using namespace std;

bool isInside(int* arr, int* ptr, int n){
    if(ptr >= arr and ptr < arr+n){
        return true;
    }
    return false;
}

int main(){
    int arr[5] = {2,3,4,5,5};
    int* ptr = arr+2;

    cout << "ptr+2: " << (isInside(arr, ptr, 5)? "Inside the Array" : "Not inside the array");
    cout << endl;
    cout << "ptr+9: " << (isInside(arr, arr+9, 5)? "Inside the Array" : "Not inside the array");
    cout << endl;

    return 0;
}
```
***
# 10. Advanced pointers and Dynamic memory
### Stack vs Heap
| Stack                         | Heap                          |
| ----------------------------- | ----------------------------- |
| Auto-managed                  | Manual using `new` / `delete` |
| Fast                          | Slower                        |
| Limited                       | Much larger                   |
| Variables die when scope ends | Lives until `delete`          |
### Dynamic memory allocation
```c++
// allocation
int *p = new int;     // raw memory
*p = 10;              // assign value

// delete
delete p;
p = nullptr;          // optional but good practice
```
### Dynamic arrays
```c++
// allocate
int *arr = new int[5];

// deallocate
delete[] arr;
arr = nullptr;
```
### Pointer arithmetic
```c++
int arr[5] = {10,20,30,40,50};
int *p = arr;
```

| Expression | Meaning                               |
| ---------- | ------------------------------------- |
| `p + 1`    | moves by 4 bytes (int) → next element |
| `*(p + 2)` | value at index 2 → `30`               |
| `p++`      | increment pointer after use           |
| `++p`      | increment pointer before use          |
### Distance between pointers
```c++
int* p = arr;       // &arr[0]
int* q = arr + 3;   // &arr[3]
cout << q - p;      // 3
```
### Why use dynamic arrays?
- Size unknown at the compile time
- Data needs to live after the function ends
- Build dynamic structures (Trees, graphs, LL)
### Pointer arithmetic

1. Creating a 2d Array using Pointer Arithmetic
```c++
#include <bits/stdc++.h>
using namespace std;

int** create2DMat(int n, int m){
    int** arr = new int*[n];
    for(int i = 0; i < n; i++){
        arr[i] = new int[m];
    }
    return arr;
}
void display(int n, int m, int** arr){
    for(int i=0; i < n; i++){
        for(int j=0; j < m; j++){
            cout << *(*(arr+i)+j) << " ";
        }
        cout << endl;
    }
}
void initialize(int n, int m, int** arr, int val){
    for(int i=0; i < n; i++){
        for(int j=0; j < m; j++){
            *(*(arr+i)+j) = val;
        }
    }
}

void delete2DMat(int n, int** arr){
    for(int i=0; i < n; i++){
        delete[] arr[i];
    }
    delete[] arr;
}

int main(){
    int n = 5;
    int m = 5;

    int** arr = create2DMat(n,m);
    display(n, m, arr);

    initialize(n,m,arr,10);
    display(n,m,arr);

    delete2DMat(n, arr);
}
```
- The line `int** arr = new int*[n];` 
	gives us  
```
[ ptr → row0 ]
[ ptr → row1 ]
[ ptr → row2 ]
[ ptr → row3 ]
```

- The line `arr[i] = new int[m];`
```
row0: [  ?  ?  ?  ?  ? ]
row1: [  ?  ?  ?  ?  ? ]
row2: [  ?  ?  ?  ?  ? ]
```
### output:
```
0 0 0 0 0 
0 0 0 0 0 
0 0 0 0 0 
0 0 0 0 0 

10 10 10 10 10 
10 10 10 10 10 
10 10 10 10 10 
10 10 10 10 10 
10 10 10 10 10 
```

2. Remove consecutive duplicates inplace
```c++
#include <bits/stdc++.h>
using namespace std;

int removeDup(int* arr, int n){
    int* write = arr;
    int* read = arr;

    while(read < arr+n){
        *write = *read;
        while(read < arr+n && *read == *write){
            read++;
        }
        write++;
    }
    return write - arr;
}

void display(int n, int* arr){
    for(int i = 0; i<n; i++){
        cout << *(arr+i) << " ";
    }
    cout << endl;
}

int main(){
    int size = 5;
    int arr[] = {1,2,2,2,5};

    display(size, arr);
    int newSize = removeDup(arr, size);

    display(newSize, arr);
}
```
***
# 11. Struct and OOPS concepts

In C++, a `struct` is a user-defined data type that groups variables together.
```c++
struct Student {
    string name;
    int age;
    float gpa;
};
```
- it bundles related data into a single unit

```c++
Student s1;
s1.name = "Arun";
s1.age = 20;
s1.gpa = 8.5;
```
### Struct vs Class
| Feature                            | `struct`            | `class`                         |
| ---------------------------------- | ------------------- | ------------------------------- |
| Default access                     | **public**          | **private**                     |
| Used mostly for                    | Plain data grouping | Full OOP (methods, abstraction) |
| Supports functions?                | Yes                 | Yes                             |
| Supports constructors/destructors? | Yes                 | Yes                             |
### Adding functions 
```c++
struct Student {
    string name;
    int age;

    void introduce() {
        cout << name << " (" << age << ")\n";
    }
};
```
### OOPS
- **Encapsulation** – data + functions together
- **Abstraction** – hiding unnecessary details
- **Inheritance** – one type derives from another
- **Polymorphism** – same function behaves differently in different classes
### Memory layout of struct
```c++
struct A {
    int x;    // 4 bytes
    char y;   // 1 byte
    double z; // 8 bytes
};
```
memory is stored contiguously with padding

```c++
A obj;
A* ptr = &obj;

cout << &obj.x;  
cout << &obj.y;
cout << &obj.z;
```

```c++
#include <bits/stdc++.h>
using namespace std;

struct Student {
    string name;
    int age;
    float gpa;

    void display() {
        cout << name << " | " << age << " | " << gpa << endl;
    }
};

void increaseAge(Student &s) {
    s.age += 1;
}

int main() {
    Student s1 = {"Arjun", 19, 8.2};
    s1.display();

    increaseAge(s1);

    s1.display();
}
```

1. Calculate Distance using points
```c++
#include <bits/stdc++.h>
#include <cmath>
using namespace std;

struct Point{
    float x;
    float y;
    void display(){
        cout << "Point: (" << x << "," << y << ")";
    }
};
float calcDistance(Point &p1, Point &p2){
    float x_squared = pow(p2.x - p1.x, 2.0);
    float y_squared = pow(p2.y - p1.y, 2.0);
    return pow(x_squared + y_squared, 0.5);
}

int main(){
    Point p1 = {10, 40};
    Point p2 = {40, 33};
    float distance = calcDistance(p1, p2);
    cout << endl;
    cout << "The distance is " << distance << endl;

    return 0;
}
```

2. Date object
```c++
#include <bits/stdc++.h>
using namespace std;

bool isLeap(int year) {
    return (year % 400 == 0) || (year % 4 == 0 && year % 100 != 0);
}

int daysInMonth(int month, int year) {
    int days[] = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
    if (month == 2 && isLeap(year)) return 29;
    return days[month - 1];
}

struct Date {
    int day, month, year;

    Date(int d, int m, int y) : day(d), month(m), year(y) {}

    bool isEarlier(const Date &other) const {
        if (year != other.year) return year < other.year;
        if (month != other.month) return month < other.month;
        return day < other.day;
    }

    Date nextDay() const {
        int d = day, m = month, y = year;

        int days = daysInMonth(m, y);

        if (d < days) {
            return Date(d + 1, m, y);
        } 
        else {
            d = 1;
            if (m == 12) {
                return Date(1, 1, y + 1);
            }
            return Date(1, m + 1, y);
        }
    }

    void print() const {
        cout << day << "/" << month << "/" << year << endl;
    }
};

int main() {
    Date d1(31, 12, 2005);

    d1.print();
    Date d2 = d1.nextDay();
    d2.print();

    cout << d2.isEarlier(d1) << endl;  // will print 0 (false)
}

```

## Classes, Objects, Constructors and deconstructors

- Class -> Blueprint
- Object -> a real thing made from the blueprint

### Class
```c++
#include <iostream>
using namespace std;

class Student {
private:
    string name;
    int age;

public:

    Student() {
        name = "Unknown";
        age = 0;
    }

    Student(string n, int a) {
        this->name = n;
        this->age = a;
    }

    Student(const Student &s) {
        name = s.name;
        age = s.age;
    }

    void display() {
        cout << name << " - " << age << endl;
    }

    ~Student() {
        cout << "Destroying object of " << name << endl;
    }
};

int main() {
    Student s1("Paradox", 19);
    Student s2 = s1; // copy constructor
    s2.display();
}
```

1. Array Class
```c++
#include <bits/stdc++.h>
using namespace std;

class Array{
public:
    int* arr;
    int size;

    Array(){
        arr = nullptr;
        size = 0;
    }
    Array(initializer_list<int> list){
        size = list.size();
        arr = new int[size];
        int i = 0;
        for(int x: list){
            arr[i++] = x;
        }
    }
    Array(Array &a){
        size = a.size;
        arr = new int[size];
        for(int i = 0; i<size; i++){
            arr[i] = a.arr[i];
        }
    }
    Array(int* src, int size){
        this->size = size;
        arr = new int[size];
        for(int i = 0; i<size; i++){
            arr[i] = *(src+i);
        }
    }
    ~Array(){
        delete[] arr;
        arr = nullptr;
        size = 0;
    }

    void show(){
        for(int i = 0; i<size; i++){
            cout << arr[i] << " ";
        }
        cout << endl;
    }
    void set(int index, int val){
        if(arr != nullptr){
            arr[index] = val;
        }
    }
    int get(int index){
        if(arr != nullptr){
            return arr[index];
        }
    }
    void flip(){
        int *front = arr;
        int *back = arr+size-1;
        int temp;
        if(front < back){
            temp = *front;
            *front = *back;
            *back = temp;

            front++;
            back --;
        }
    }
};

int main(){
    Array a1({1,2,6,9,5});
    int src[] = {1,2,4,7,3,5,9};
    Array a2(src, 7);
    a2.show();
}
```

## Encapsulation, const, operator overloading
### Encapsulation
it means making the class safe.
```c++
public:
    int* arr;
    int size;
```
- anyone can modify the `arr` and `size` variables.

```c++
class Array {
private:
    int* arr;
    int size;

public:
    // constructors, destructors, methods…
};
```
### Const usage

1. Put const in front of methods that DO NOT modify the object
```c++
int get(int i) const;
void show() const;
int operator[](int i) const;
bool operator==(const Array& other) const;
```
because these methods only read data and don't modify objects
### Operator overloading
Assigning custom functionalities to operators so they make the object's of the class behave naturally

```c++
int operator[](int i) const {
    return arr[i];
}
```
will let us do,

```c++
a1[2] = 10;
cout << a1[2];
 ```

1. Implementing deep copy with `=` operator
```c++
Array& operator=(const Array& other) {
    if (this != &other) {
        delete[] arr;   // clear old memory
        size = other.size;
        arr = new int[size];
        for(int i = 0; i < size; i++) arr[i] = other.arr[i];
    }
    return *this;
}
```

so this would work
```c++
Array a2 = a1;
Array a3;
a3 = a1;
```

2. Working with `<<` operator
```c++
friend ostream& operator<<(ostream& os, const Array& a) {
    for(int i = 0; i < a.size; i++) os << a.arr[i] << " ";
    return os;
}
```

3. Working with `==` operator
```c++
bool operator==(const Array& other) const {
    if (size != other.size) return false;
    for(int i = 0; i < size; i++)
        if (arr[i] != other.arr[i]) return false;
    return true;
}
```
### Inheritance
```c++
class Animal {
public:
    void eat() { cout << "Eating...\n"; }
};

class Dog : public Animal {
public:
    void bark() { cout << "Barking...\n"; }
};
```
### Function Overriding
```c++
class Animal {
public:
    virtual void sound() { cout << "Some sound\n"; }
};

class Dog : public Animal {
public:
    void sound() override { cout << "Woof!\n"; }
};
```
### Abstract class
```c++
class Shape {
public:
    virtual void draw() = 0;  // pure virtual function
};
```
- Any class with at least 1 pure virtual function → abstract class.
Derived classes must implement it
```c++
class Circle : public Shape {
public:
    void draw() override {
        cout << "Drawing circle\n";
    }
};
```

Polymorphism
```c++
Shape* s1 = new Circle();
Shape* s2 = new Rectangle();

s1->draw(); // Circle's implementation
s2->draw(); // Rectangle's implementation
```
***
# STL Containers
Standard Template Library that contains reusable data structures and algorithms.

It has 3 big parts
- Containers -> vector, map, set, etc
- Iterators -> pointer like objects
- Algorithms -> sort(), find(), etc

### 1. Vector (dynamic array)
```c++
vector<int> v;
vector<int> v = {1,2,3};
```

important functions
```c++
v.push_back(x);
v.pop_back();
v.size();
v.empty();
v.front();
v.back();
v[i];
v.clear();
v.insert(v.begin() + index, value);
v.erase(v.begin() + index);
```
##### Time complexities
- push_back -> `O(1)`
- random access -> `O(1)`
- insert / erase in the middle -> `O(n)`

### 2. Deque (double ended queue)

Supports push and pop from both sides, efficiently.
```c++
deque<int> d;
d.push_back(10);
d.push_front(5);
d.pop_back();
d.pop_front();
```

- When you need fast insertions from both sides
- `vector` fails for front insert (O(n))
- `deque` does it in O(1).

### 3. List (doubly linked list)
```c++
list<int> l;
l.push_back(10);
l.push_front(20);
l.insert(next(l.begin(), 2), 99);
l.erase(l.begin());
```
- Insertion anywhere is only `O(1)`
but,
- No indexing
- No caching -> Slower than vector

use only when fast middle insert/delete is needed.

### 4. Set and Unordered Set
##### Set
- Sorted
- Unique elements
- Backed by Red-Black Tree (self-balancing)
- O(log n) insertion/search
```c++
set<int> s;
s.insert(10);
s.insert(5);
s.insert(10); // ignored
s.erase(5);
```
##### Unordered set
- Not sorted
- Uses Hash Table
 - O(1) average time
- Worst case O(n)
```c++
unordered_set<string> us;
us.insert("hello");
us.insert("world");
```

- Use unordered_set for speed.
- Use set when sorted order is needed.

### 6. MAP and UNORDERED_MAP
- Sorted keys
- Key-value pair
- O(log n) operations
#### Map
- Sorted keys
- Key-value pair
- O(log n) operations
```c++
map<string, int> mp;
mp["apple"] = 120;
mp["banana"] = 40;
```
#### Unordered map
- Hash table
- O(1) average
- No sorting
```c++
unordered_map<int, string> ump;
ump[101] = "Alex";
```

### When to use what?

|               | Sorted? | Allows duplicate? | Speed              |
| ------------- | ------- | ----------------- | ------------------ |
| vector        | No      | Yes               | Fastest for access |
| deque         | No      | Yes               | Fast at both ends  |
| list          | No      | Yes               | Fast middle insert |
| set           | Yes     | No                | log(n)             |
| unordered_set | No      | No                | O(1) average       |
| map           | Yes     | No                | log(n)             |
| unordered_map | No      | No                | O(1) average       |
### STL patterns
| Pattern                | STL Used              |
| ---------------------- | --------------------- |
| Frequency counting     | `unordered_map`       |
| Unique elements        | `set`                 |
| Sorting problems       | `vector + sort`       |
| Binary search problems | `lower_bound`         |
| Sliding window         | `map / unordered_map` |
| Top K problems         | `priority_queue`      |
***

# Unordered_map
Its an associative container that stores elements formed by the combination of a key and a mapped value. It uses Hashing technique to store and retrieve elements extremely quickly.
- The hashing function uses Separate chaining (Linked lists) to handle collision handling. 

## Thinking in STL terms

## Frequency counting
use `unordered_map` or `map` for frequency counting.
`map` -> sorted
`unordered_map` -> unsorted

1. Given an array of integers, find the **frequency of each element**.
```c++
Input:  [1, 2, 2, 3, 1, 4, 2]
Output:
1 -> 2
2 -> 3
3 -> 1
4 -> 1
```
- Do I need ordering? => No (but if so, then => ==MAP.==)
- Do I need fast lookup => YES
- Am I Counting occurrences? => YES.
#### THIS IS A FREQUENCY PROBLEM.

```c++
    vector<int> arr = {1,5,3,5,7,8,5,3,5};
    map<int,int> freq;
    for(int x: arr){
        freq[x]++;
    }
    for(auto &p: freq){
        cout << p.first << ": " << p.second << endl;
    }
```

2. Anagram problem
(same characters with same frequencies, order doesn’t matter)
- Does order matter? NO.
- Does count matter? YES.
This is also frequency problem.

```c++
#include <bits/stdc++.h>
using namespace std;

bool isAnagram(string s, string t){
    if(s.size() != t.size()) return false;

    unordered_map<char, int> freq;

    // incrementing with first string
    for(char x: s){
        freq[x]++;
    }

    // decrementing with second string
    for(char x: t){
        if(--freq[x] < 0) return false;
    }
    return true;
}

int main(){
    cout << isAnagram("silent", "listen") << endl;
    cout << isAnagram("rat", "car") << endl;
}
```

3. Majority element
Given an array of size n, find the element that appears more than ⌋n/2⌊ times. You may assume such an element always exists.

`⌋n/2⌊` -> Flooring the n/2 value to its nearest whole number. So Each element must appear `⌋n/2⌊ + 1`. That `+1` is because of `more than ⌋n/2⌊ times` phrase.

| **Array Size (n)** | **n/2** | **⌊n/2⌋** | **Required Frequency (More Than ⌊n/2⌋)**                     |
| ------------------ | ------- | --------- | ------------------------------------------------------------ |
| 5                  | 2.5     | 2         | **3** (must appear $\lfloor 5/2 \rfloor + 1 = 3$ times)      |
| 6                  | 3.0     | 3         | **4** (must appear $\lfloor 6/2 \rfloor + 1 = 4$ times)      |
| 7                  | 3.5     | 3         | **4** (must appear $\lfloor 7/2 \rfloor + 1 = 4$ times)      |
| 10                 | 5.0     | 5         | **6** (must appear $\lfloor 10/2 \rfloor + 1 = 6$ times)<br> |

```c++
#include <bits/stdc++.h>
using namespace std;

int majorityElement(vector<int>& nums) {
    unordered_map<int, int> freq;
    int n = nums.size();

    for (int x : nums) {
        freq[x]++;
        if (freq[x] > n / 2)
            return x;
    }

    return -1; // won't happen (guaranteed)
}

int main() {
    vector<int> v = {2,2,1,1,1,2,2};
    cout << majorityElement(v) << endl;
}
```

4. Majority element using Sorting + vector

```c++
#include <bits/stdc++.h>
using namespace std;

int majorityElement(vector<int> &nums){
    sort(nums.begin(), nums.end());
    return nums[nums.size()/2];
}

int main(){
    vector<int> nums = {1,5,7,3,3,4,6,7,4,4,3,3,3,3,3,3,3,3,3};
    cout << "The majority element is: " << majorityElement(nums) << endl;
}
```

4. Two Sum sorted array
```c++
#include <bits/stdc++.h>
using namespace std;

void display(const vector<int> &nums){
    for(int i: nums){
        cout << i << " ";
    }
    cout << endl;
}

vector<int> sortArr(vector<int> &nums){
    sort(nums.begin(), nums.end());
    return nums;
}

vector<int> majorityElement(vector<int> &sorted_nums, int two_sum){
    int start = 0;
    int end = sorted_nums.size()-1;
    for(int i = 0; i<end; i++){
        int sum = sorted_nums[start] + sorted_nums[end];
        if(sum == two_sum) return {sorted_nums[start], sorted_nums[end]};
        else if(sum < two_sum) start++;
        else end--;
    }
    return {0,0};
}

int main(){
    vector<int> nums = {1,4,7,5,3,3,4,5,6,8,7,6,5,2,1,2,3,2};

    sortArr(nums);
    vector<int> index = majorityElement(nums, 10);
    display(index);
}
```

5. Two sum using two pointer
```c++
#include <bits/stdc++.h>
using namespace std;

void display(const vector<int> &nums, int end=0){
    if(end==0) end = nums.size();
    for(int i = 0; i<end; i++){
        cout << nums[i] << " ";
    }
    cout << endl;
}
int removeDupes(vector<int> &nums){
    int i = 0;
    for(int j = 1; j < nums.size(); j++){
        if(nums[i] != nums[j]){
            i++;
            nums[i] = nums[j];
        }
    }
    return i+1;
}

void sortArr(vector<int> &nums){
    sort(nums.begin(), nums.end());
}

vector<int> twoSum(vector<int> &sorted_nums, int two_sum){
    int i = 0;
    int j = sorted_nums.size()-1;
    while(i < j){
        int sum = sorted_nums[i] + sorted_nums[j];
        if(sum == two_sum) return {sorted_nums[i], sorted_nums[j]};
        else if(sum < two_sum) i ++;
        else j --;
    }
    return {0,0};
}

int main(){
    vector<int> nums = {1,4,7,5,3,3,4,5,6,8,7,6,5,2,1,2,3,2};

    sortArr(nums);
    removeDupes(nums);
    display(twoSum(nums, 10));
}
```

6. Three sum 
```c++
#include <bits/stdc++.h>
using namespace std;

void sortArr(vector<int> &nums){
    sort(nums.begin(), nums.end());
}

vector<vector<int>> threeSum(vector<int> &arr){
    vector<vector<int>> res;

    // 1. Sort the list
    sort(arr.begin(), arr.end());
    int n = arr.size();
    
    // 2. fix first elements
    for(int i=0; i<n-2; i++){
        if(i > 0 && arr[i] == arr[i-1]) continue;

        int l = i+1;
        int r = n-1;

        // 3. two pointers
        while(l < r){
            int sum = arr[i] + arr[l] + arr[r];

            if(sum == 0){
                res.push_back({arr[i], arr[l], arr[r]});

                while(l < r && arr[l] == arr[l+1]) l++;
                while(l < r && arr[r] == arr[r-1]) r--;

                l++;
                r--;
            }
            else if(sum < 0) l++;
            else r--;

        }

    }
    return res;
}

int main(){

    vector<int> nums = {-1,0,1,2,-1,-4};

    vector<vector<int>> res = threeSum(nums);

    for(auto vec: res){
        for(int x: vec){
            cout << x << " ";
        }
        cout << endl;
    }
    return 0;
}
```

#### four sum problems algo
1. Calculate the array size
2. sort the array
3. iterate through each element with for loop (i). End before 3 elements
	- for each element, check if the previous element is the same. If so increment i by 1
4. Iterate through each element again with for loop (j). End before 2 elements
	- for each element, check if the previous element is the same. If so increment j by 1
5. Define two variables `l = j+1` and `r = n-1` 
6. while `l < r`,  calculate `sum = nums[i] + nums[j] + nums[l] + nums[r]`
	- if `sum == 0`, 
		- add it to the result list
		- check if there are duplicate elements from `l` side, increment to skip them
		- check if there are duplicate elements from `r` side, decrement to skip them
		- do `l++` and `r--` to continue with the algorithm
	- if `sum < 0`, then `l++`
	- if `sum > 0`, then `r--`

7. Four sum
```c++
#include <bits/stdc++.h>
using namespace std;

vector<vector<int>> fourSum(vector<int> &arr){
    int n = arr.size();
    sort(arr.begin(), arr.end());

    vector<vector<int>> res;
    if(n < 4) return res;

    for(int i = 0; i<n-3; i++){
        if(i > 0 && arr[i] == arr[i-1]) continue;
        for(int j = i+1; j < n-2; j++){
            if(j>i+1 && arr[j] == arr[j-1]) continue;

            int l = j+1;
            int r = n-1;

            while(l < r){
                long long sum = (long long) arr[i] + arr[j] + arr[l] + arr[r];
                if(sum == 0){
                    res.push_back({arr[i], arr[j], arr[l], arr[r]});

                    while(l < r && arr[l] == arr[l+1]) l++;
                    while(l < r && arr[r] == arr[r-1]) r--;

                    l++;
                    r--;
                }
                else if(sum < 0) l++;
                else r--;
            }
        }
    }

    return res;
}

int main(){
    vector<int> nums = {-1,2,4,1,1,-2,-1,-1,0,3,4,-2,-3,-4,1};
    vector<vector<int>> res = fourSum(nums);

    for(auto &triplets: res){
        for(int elem: triplets) cout << elem << " ";
        cout << endl;
    }

    return 0;
}
```