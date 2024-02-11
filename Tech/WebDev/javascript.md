## datatypes
==Not like C, variables can store any datatype values;==
- number (All the numbers, decimals included are considered within this one category) [** is exponent.]
- string
- null
- boolean
- undefined - NaN (NaN stands for Not a Number, but it's considered within the number datatype. ==Those javascript memes are beginning to make sense..==)
```js
console.log('can print something');
let input = prompt("Ben, say something.. ");

//this extracts number from the string, returns NaN if there's no number
parseInt('123asdf'); //outputs 123
typeof something //return the datatype
```
## declaring 
```js
let num = 3;
const speedOfLight = 299792458; // constant, cannot change
let isCap = true, isCap = false;

// old way of doing things
var num = 3;
```
## string methods
```js
let string = "HelloThere";

string.length // gives len, no ().
string.toUpperCase();
string.toLowerCase();
string.trim(); // works like strip() in python
string.indexOf('wordToSearch');
string.slice(startIndex, endIndex);
string.replace(whatToReplace, whatToReplaceWith); //replaces only the first occ
string.repeat(timesToRepeat)

//formated string
let genName = "Kenobi";
//notice the back-tick, only they evaluate the string template, normal quotes won't cut it.
`Hello There! general ${genName}`;
```
## control statements
```js
if (condition){
	statements;
}
else if (condition){
	statements;
}
else{
	statements;
}

// note
// if a variable is declared inside the if block, it cannot be accessed from outside, its called block scope.
//eg 
if(true){
	let hi = 'hi'
}
console.log(hi) //returns an error
```
## logical operators
```js
&& // And
|| // Or
! //Not

// this is strict equal to (taking into account the memory address of both the values, if they're stored in the same place, then it returns True)
===
```
## try and catch
```js
//like try and finally in python, used for error management

try{
	statements;
} catch (e) {
	console.log(e) //catches the error and prints it, this is                           different from the normal as program stops                         normally.
	statements;
}
```
## arrays
```js
let array = ["Hello","There"];
//nested arrays
let nestedArrays = ['hi',['hello','what'],['yello']];

array[0] = 'Hi';

array.push("!"); // adds to the end of list
array.unshift("Yo") // adds to the start of list
array.pop(); // deletes the end element
array.shift(); // deletes the start element

let array3 = array1.concat(array2);
array.includes("Hello"); // true, element "Hello" is in the list
array.indexOf(element);
array.reverse(); // in-place and affects original
array.slice(startIndex, endIndex); // deletes the elements till indexNum and returns rest of the elements
array.splice(indexToInsert, countOfElements_ToDeleteThere, elementToInsert, elementsToInsert);
```
## math module and random library
```js
// access pi value from Math lib
Math.pi
//just cuts the decimal part
Math.floor(2.4444) // is 2
// just rounds it up
Math.ceil(3.1) // is 4
// gives a random value between 0 and 1 (0.1-0.9)
Math.random()

// so to get a integer value between 1 and 10
Math.floor(Math.random()*10)+1
// so to get a integer value between 1 and 5
Math.floor(Math.random()*5)+1
Math.pow(number,exponent)
```
## object literal
==hold those horses, I thought this what Oops, but nah this is just python's dictionary equivalent datatype.==

```js
// note keys dont have to be in strings they are automatically converted!
const fitBitData = {
	totalSteps : 65535,
	totalMiles : 299.792458,
	avgCalorieBurn : 10000,
	workOutsThisWeek : '4 of 10',
	avgGoodSleep : NaN;
}

// to call a value
fitBitData['totalSteps']
// or
fitBitData.totalSteps

//to add elements to an object. Key should be in a string.
fitBitData['GoodGod'] = '3'
fitBitData.'GoodGod = 3

//functions
Object.keys(object_name)
Object.values(object_name)
Object.entries(object_name)
```
## loops
```js
// the mighty for loop
for(initialization;condition;creement){
	statements;
}

for(let i=0;i<9;i++){
	statements;
}

// the mighty while loop
let i = 0;
while(i<100){
	statements;
	i++;
}

// The Almight for of loop (this is seriously great)
for(let tempVar of iterable){
	statements;
}
//to iterate over an object
for(let key in objectName){
	statements;
}

//foreach
iterable.forEach(function(a){
	statements; //forEach will feed new elements in each iteration to a
})

//map function - returns an array of new calculated values based on the prev array
newArray = iterable.map(function(tempVar){
	return statement;
})
newArray = iterable.filter(function(tempVar){
	return conditionalStatement;
})

//together goodness
newArray = arr.filter((x) => x.release_date<50).map((x) => x.movie_name)

//some and every functions
arr=[1,2,3,4,5,6,7,8,9]
arr.some(x => x<7) //returns true
arr.every(x => x<7) //returns false

//reduce em down to the ashes of its very creation
arr.reduce((accumulator, element) => element+accumulator,initial_value_for_accumulator)

```
## functions
```js
//defining funcitons
function functionName(parameters){
	//Ben, do something.
	return something;
}

//calling the function
functionName(arguments)

//function expresion - another way of defining a function
const add = function(a,b){
	return a+b;
}

//higher order functions - passing functions to functions.
function callnTimes(n,func){
	for(let i=0;i<n,i++){
		func();
	}
}
function func(){
	console.log('Hello there');
}
callnTimes(9,func);

//returning functions
function theHeadwig(num){
	if(num>3){
		return function(){
			console.log("Nah, hardpass");
		}
	}
	else if(num<3){
		return function(){
			console.log("Common, its a narrow hit");
		}
	}
	else{
		return function(){
			console.log("There, that, Now my friend. We arrived");
		}
	}
}
let chosenFunction = theHeadwig(3);

//newer way of defining functions
//arrow functions
let newFunc = (x,y) => {
	return statements;
}
let newFunc = () => {
	return statements;
}
//or if only one parameter is present, no need for ()
let newFunc = x => {
	return statements;
}
//implicit returning with arrow functions. Note the braces.
let newFunc = x => (
	statements;
)
// one-liner with implicit returning
let newFunc = x => statement;
//the keyword this behaves differently in an arrow function and in a regular function.
```
## methods (functions inside object)
```js
const math = {
	PI: 3.14,
	SPEEDOFLIGHT: 299792458,
	multiply: function(a,b){
		return a*b;
	},
	divide: function(a,b){
		return a/b;
	},
	power: function(a,e){
		let power = 1;
		for(let i=0;i<e;i++){
			power *= a;
		}
		return power;
	}
}

math.SPEEDOFLIGHT // gives 299792458
math.power(2,4) // gives 16

//this keyword - to reference the methods or properties within a method, and only a method.
const snake = {
	name: "Hisssenbuurp",
	age: "foreva",
	peopleAte: '13 civilizations and counting',
	size: 'half of Jormungandr',
	description: function(){
		console.log(`${this.name} is ${this.size}, now at the age of ${this.age}, she ate ${this.peopleAte}.`);
	}
}
```
## setTimeout and setInterval
```js
setTimeout(function(),milliseconds) // executes the function only once
setInterval(function(),milliseconds) // executes the function every milliseconds 
```