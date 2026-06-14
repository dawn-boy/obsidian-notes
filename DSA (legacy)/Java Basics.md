## String Functions
```java
String text = "hello";
int len = text.length(); // len is 5

String emptyStr = "";
boolean isEmpty = emptyStr.isEmpty(); // isEmpty is true

String word = "Java";
char firstChar = word.charAt(0); // firstChar is 'J'
```
### Comparisons
```java
String s1 = "hello";
String s2 = "hello";

boolean areEqual = s1.equals(s2); // areEqual is true
boolean areEqual = s1.equalsIgnoreCase(s2); // areEqual is true

String sentence = "The quick brown fox.";
boolean hasFox = sentence.contains("fox"); // hasFox is true

String filename = "document.txt";
boolean isTextFile = filename.endsWith(".txt"); // isTextFile is true

String data = "banana";
int index = data.indexOf("an"); // index is 1
```
### Actions
```java
String msg = "Hello World";
String upper = msg.toUpperCase(); // upper is "HELLO WORLD"

String padded = "   Java is fun   ";
String trimmed = padded.trim(); // trimmed is "Java is fun"

String phrase = "Programming";
String sub1 = phrase.substring(4); // sub1 is "amming"
String sub2 = phrase.substring(0, 4); // sub2 is "Prog"

String original = "Java";
String modified = original.replace('a', 'o'); // modified is "Jovo"

String fruits = "apple,banana,orange";
String[] fruitArray = fruits.split(","); // fruitArray is ["apple", "banana", "orange"]

String firstName = "John";
String fullName = firstName.concat(" Doe"); // fullName is "John Doe"
```

## StringBuilder class
- StringBuilder offers a mutable sequence of characters compared to the usual String class
## Code
```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World"); 
// sb now contains "Hello World"

StringBuilder sb = new StringBuilder("Java is great");
sb.insert(5, "very ");
// sb now contains "Java very is great"

StringBuilder sb = new StringBuilder("Programming");
sb.delete(3, 7);
// sb now contains "Proing"

StringBuilder sb = new StringBuilder("hello");
sb.reverse();
// sb now contains "olleh"

StringBuilder sb = new StringBuilder("Final result");
String result = sb.toString();
```

- Use string when we need a simple, unchangeable set of chars
- Use StringBuilder when we need to modify the string

```java
// Inefficient with String
String s = "";
for (int i = 0; i < 1000; i++) {
    s += "a"; // Creates a new String object in each iteration
}

// Efficient with StringBuilder
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 1000; i++) {
    sb.append("a"); // Modifies the same object
}
```
***
# Methods
Method definition would look like
```java
public static void myMethod(int param1, String param2) {
    // Code to be executed
}
```
- **`public`**: An access modifier that makes the method accessible from any other class.
- **`static`**: A keyword indicating the method belongs to the class, not to an instance of the class. You can call a `static` method without creating an object of the class.
## Pass by Value
Java is always **pass by value**. This means that when you pass an argument to a method, a **copy** of the value is made and passed to the method's parameter.

## Method Overloading
**Method overloading** is a feature that allows a class to have multiple methods with the same name but different parameters. 
```java
public class MathUtils {
    // Method to add two integers
    public int add(int a, int b) {
        return a + b;
    }

    // Overloaded method to add three integers
    public int add(int a, int b, int c) {
        return a + b + c;
    }

    // Overloaded method to add two doubles
    public double add(double a, double b) {
        return a + b;
    }
}
```
## Recursion
- recursion is a programming technique where the method calls itself to solve a problem.
```java
public class Factorial {
    public static int factorial(int n) {
        // Base case: If n is 0 or 1, return 1
        if (n <= 1) {
            return 1;
        }
        // Recursive step: Call the method with a smaller input
        else {
            return n * factorial(n - 1);
        }
    }

    public static void main(String[] args) {
        int result = factorial(5); // Calculates 5 * 4 * 3 * 2 * 1
        System.out.println(result); // Output: 120
    }
}
```

