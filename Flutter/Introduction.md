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