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
# Strings
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