```dart
void main(){
	print("Hello");
	print(4);
	
	print(''' hello
	something''');
	print("helo \n world");
}
```

## Declaration
```dart
// <datatype> <variable_name> = value;
int something = 3;
double something = 4;

String something = "Hello";
bool something = true; 

// can take any value
dynamic whatever = 23;
dynamic whatever = true;

// inference by dart
var somevalue = 12;
final somevalue = 10; // run-time constant
const somevalue = 30; // compile-time constant

// optional variable
int? somevalue; // ? allows for null value
print(somevalue?.length) // retuls null during null cases
```

#### Formatted string
```dart
void main() {
  String name = "Adithya";
  
  String greetings = "HEllo ${name}";
  String greetings = "HEllo $name";
  
  print(greetings);
}
```

#### if else
```dart
if(age>=18 && true){
	//body
} else if(age>=21 || false){
	//body
} else{
	//body
}
```

#### ternary
```dart
String value = somevalue.startswith("H") ? 'wow' : 'nah' ;
```

#### switch statement

```dart
// no need to write break for non-empty body

switch(someValue){
	case 'Hi':print(print("print("hello");
		print("hello");
		hello");
		"hello");
		
		print("hello");
		
	case 'hel' when age>=20:
		print("Good");
		
	case 'ho': break;
	
	default: 
		print("okay");
}
```

#### For loop
```dart
for(int i=1; i<10; i++){
	//body
}
while(condition){
	//body
}
```

### Functions
```
void main(){
    String? name = printName();
    var data = data();
    var (age, name) = data();   #this is data unpacking
    print(data.$1); #this gives 12
  }

String printName(){
  return "Helo";
  }

(int, String) data(){
  return (12, "helo");
  }
```
### Parameters
```
void main(){
 greetings(true, name: "Sara", age: 39); 
}

void greetings(bool isAdult, {required String name, int? age}){      #here age is optional and isAdult is not a positional argument.
  print("${name} is ${age}");
}
```
## Classes
```
void main(){
  Cookie cookie = Cookie();
  final cookie_2 = Cookie();
  cookie.baking();
  print(Cookie.name);
}

class Cookie{
    #variables
    String? shape;
    double? size;
    static String name;

    #constructor
    Cookie(this.shape, this.size){
      //body
    }

    #private variables
    double _height = 4;
    double _widht = 2;

    #Getters
    int get height => _height; 
    #Setters
    set setHeight(double height){
      this._height = height;
    }

    #methods
    void baking(){
      print("baking has started");
    }

    bool isCooking(){
      return false;
    }

    @override
    String toString() => '$name is of shape $shape and size $size';
}
```
## Generics class
```
void main(){
  final student = Student(30);   #class is Student<int>
  final student_2 = Student("Hello");   #class is Student<String>
  final student_3 = Student<bool>(true);  #object is initiated manually with bool generics
}

class Student<T>{
  final T name;
  Student(this.name){}
}
```

## Inheritance
```
void main() {
  final volvo = Truck("Volvo", 2023, "Black", 1009);
  print(volvo.color);
}

class Vehicle {
  String _brand = "Toyato";
  int _year = 1025;
  String _color = "Black";

  Vehicle(this._brand, this._year, this._color) {
    displayInfo();
  }

  void displayInfo() {
    print("Brand: $_brand, Year: $_year, Color: $_color");
  }

  get brand => _brand;
  get year => _year;
  get color => _color;
}

abstract class VehicleStrucutre {
  abstract String _brand;
  abstract int _year;
  abstract String _color;
}

class Truck extends Vehicle implements VehicleStrucutre {
  int _payloadCapacity = 1000;

  @override
  String _brand = "Volvo";

  Truck(String brand, int year, String color, this._payloadCapacity)
    : super(brand, year, color);

  void displayInfo() {
    super.displayInfo();
    print("Payload Capacity: $_payloadCapacity");
  }

  get payloadCapacity => _payloadCapacity;
  set payloadCapacity(int value) => _payloadCapacity = value;
}

```
- Abstract classes only define the structure
- final keyword is only used to lock in the container. but you're free to change the contents of the container
- static keyword means the value of the varible declared can be accessed without having to initialize an object for that class
- dynamic keyword isnt related to static. It is used to dynamically detect the variable type
- @override is an annotation used to override funtions
- implementing a class means you must have the structre of a given class and must surely override it.
- extending a class means you inherit all the values from parent class
- one cannot implement and extend the same class. 

## Object oriented programming
```
void main() {
  #Polymorphism
  Cat cat = Cat();
  cat.sound();
  Dog dog = Dog();
  dog.sound();

  #Abstraction
  Animal animal = Cat();
  animal.sound();
  animal = Dog();
  animal.sound();
}

class Animal {
  void sound() {
    print('Animal making sound');
  }
}

class Cat extends Animal {
  @override
  void sound() {
    print('Cat making sound');
  }
}

class Dog extends Animal {
  @override
  void sound() {
    print('Dog making pound');
  }
}
```
## Mixins
- kinda similar to extending a class but without the parent-child relationship. this is only used to mash in potatoes.. no heirarchies.
```
void main() {
// mixin
// mixes in
final anim = Animal();

anim.fn();

}

mixin Jump {
int jumping = 18;

}

mixin Screamf{
bool isScreaming = false;

}

class Animal with Jump, Scream {
void fn() {
print(jumping);
print(isScreaming);
}
```
## Class modifiers
```
void main() {
Animal animal = Cat();

switch(animal) {
  case Dog():
    print('dog');
  case Cat():
    print('cat');
  case Human():
    print('human');
}

sealed class Animal{}
final class Animal1{}

class Human implements Animal {}
class Dog implements Animal {}
class Cat extends Animal {}
```
- sealed class ensures that it cannot be implemented in any other libraries. You must implement in the same file.
- abstract and sealed classes cannot be constructed in main. Final classes can be constructed.
- extending a `base, final, sealed` class must also have specification on whether it is a `base, final, sealed`
- interface classes cannot be extended but can be implemented and constructed. 
- mixin classes have to use `with` keyword to mix-in data to another class.

## List
```
void main(){
  List myList = [1,2,3, "Hello", true];
  List myList_2<int> = [1,2,3]       #Generics constricted
  print(myList[0]);
}
```
## Futures
This is just promises. 
```
void main() async {
// Futures (Promises)

print('Hello!!!!");

giveAResultAfter2Sec().then((val) {
print(val); 1

i

print('Hey');
print('Hello');
print('Greetings!');

}

Future<String> giveAResultAfter2Sec() {
return Future.delayed(Duration(seconds: 2), () async {

Hi
}
```
## Streams
```
void main() async {
    //streams
    
    countdown().listen((value) {
        print(value);
    }, onDone: () {
        print("Done");
        },
    );
}

Stream<int> countdown(){
    for(int i = 10; i >= 0; i--){
        yield i; 
        await Future.delayed(Duration(seconds: 1));
    }
}

```