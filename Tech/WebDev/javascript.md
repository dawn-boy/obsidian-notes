0# datatypes
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
let array = ["Hello","There",'Something','in','the','way'];
//nested arrays
let nestedArrays = ['hi',['hello','what'],['yello']];

array[0] = e'Hi';

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

// arrays destructuring

//simply put their just unpacking like in python
let greet = array[0] //greet has 'Hello'
let greet_two = array[1] // greet_two has 'There'

//same can be done like this.
let [greet, greet_two, ...rest] = array; //neat.
// just to clarify, rest now has all rest of the elements in an array.
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
// ... spreads the array, giving just an array will not work, Math.min or Math.max is expecting each number in a single argument. So the ... spreads the array as arguments.
Math.max(...array)
Math.min(...array)
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
fitBitData.GoodGod = 3

//functions
Object.keys(object_name)
Object.values(object_name)
Object.entries(object_name)

//objects destructuring

//the usual way, long 
const totalSteps = fitBitData.totalSteps
const totalMiles = fitBitData.totalMiles
// the new kid
const {totalSteps, totalMiles} = fitBitData // the naming of the variable is important here, it should correspond with property of the object.
// but if you need to rename those vars without having to write another line of code. 
const {totalSteps: step_count, totalMiles: mile_count} = fitBitData

// to give a default value incase the object dont have the value

const{totalSteps = 'Nope', totalMiles} = fitBitData
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

// The Almighty for of loop (this is seriously great)
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
	return conditional'Statement;
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
function functionName(parameters=default_val){
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
			console.log("There, that, Now my friend. We've arrived");
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

// O great arguments, the array-like thingy within functions that keeps track of all the arguments passed to a function. Not available in arrow functions tho.
function something(){
	console.log(arguments)
}
something(1,2,3,4,5,6,7,8,9,0); // will output an array-like datatype containing all the arguments

//function destructuring
object = {
name: 'unbo',
lastName: 'bonbon',
age: 'yet to be born',
died: 'tomorrow'
}

// the object is destructured at the parameters section itself.
function me({name, lastName}){
	return `${name} {lastName}`
}

```
## spread and rest
```js
// in a function
Math.max(...array)
// in a list
arr = ['hi','no','yes','hono']
arr2 = [...arr] // this will just spread all the elements of arr to arr2

//in an object
new_object = {hi:12,no:34,wha:34,nop:3,as:5}
newest_object = [...new_object]

//rest - collects the rest of values
// O great rest, the actual array that helps arguments thingy live
function something(...num){
	console.log(num) // this prints out a num array which has all the arguments given to this function.

function something(parameter1, parameter2, ...rest_of_the_parameters_array){
	something; 
}

}
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

## Document Object Model (DOM)
```js

document.all // returns a list of all the available element objects

// but you can index each element in your html
document.all[0].innerHTML = 'somethin' // indexing the 0th element and changing its value to something

//selecting

getElementById(id_name)
getElementsByTagName(tag_name)
getElementsByClassName(class_name)

// new way to select a single element

document.querySelector('tag_name')
document.querySelector('#id_name')
document.querySelector('.class_name')

document.querySelector('img:nth-of-type(2)')
document.querySelector('a[title="java"]') //selects only those a tags with 'java' as title

//desendence selection
document.querySelectorAll('p a') // all a tags within a p tag

// selects all..
document.querySelectorAll(stuff)

element = document.querySelector(something)

element.innerText // gives only the visible text within 
element.textContent // gives all the text within 
element.innerHTML // allows you to directly make changes with HTML syntax

element.getAttribute(attribute)
element.setAttribute(attribute,new_value)

// change styles
element.style.color = 'blue' 

// but normally styles are not read from the separate stylesheets but rather only from the inline styles. So to get the current styles of an element..
window.getComputedStyle(element).property

// to change the class of an element
element.classList.add(new_class_name)
element.classList.remove(class_name)

element.classList.contains(class_name) // if the element has the class
element.classList.toggle(class_name) //adds the class, if not present. or deletes the class if present

//traversing
element.parentElement // every child only has one direct parent
element.childElementCount
element.children

element.nextElementSibling
element.previousElementSibling

//creating an element
document.createElement(tag)
document.body.appendChild(new_element)

p.append('para text')
p.appendChild(element)
p.prepend('ho')

element.insertAdjacentElement(type,new_element) // types: beforebegin, afterbegin, beforeend, afterend, 

// to remove the child element
child = document.querySelector(tag)
parent = child.parentElement
parent.removeChild(child)
// new way
child.remove()
```
### DOM events
```js
// inline event
<button onclick="alert('something');">hi</button>

// property events
const button = document.querySelector("#but");
button.onclick = () => {
	console.log("Hi");
}
// property listeners like onclick can have only one callback function

function twist(){
	console.log('twist');
}
function turn(){
	console.log('turn');
}

button.onclick = twist;
button.onclick = turn;
// now, onclick can house only one function either twist or turn. not both.

//EventListeners can house multiple callback function
button.addEventListener('click',twist);
button.addEventListener('click',turn);
// to run only once and then remove the eventListener
button.addEventListener('click',twist, {once : true});

//this keyword

function off(){
	this.style.color = 'red';// since this keyword is used, we can reuse this on any object
}

for(let button of buttons){
	button.addEventListener('click',off);
	otherElem.addEventListener('click',off); // reuse like so
}

button.addEventListener('keydown',somethin(e){
					console.log(e.code); // it gives the code
					console.log(e.key); // it gives the key
}); // there's keydown, keyup, keypress
```
## form events
```js
// to avoid the default page redirect behaviour of forms
form = document.querySelector('form');
input = document.querySelector('#input');
list = document.querySelector('#list');

form.addEventListener('submit', (e) => {
	e.preventDefault(); // this prevents the default actions.

	// if the form had an input box, then get value from the input

	//either direct access like,
	console.log(input.value);
	//or indirectly accessing it from forms,
	console.log(form.elements.input.value) //input is the id name.

	//if we need to append elements inside of another elements
	newli = document.createElement('li');
	newli.innerText = input.value;
	list.append(newli); // you can also prepend

})
//to remove LIs

li = document.querySelectorAll('li');
for(let list of li){
list.addEventListener('click', () => {
	list.remove();
})

//to remove LIs that were added dynamically through inputs
// this is event delegation
list = document.querySelector("#list");
list.addEventListener('click', (e) => {
	e.target.remove();
	// to make actions on certain condition
	e.target.nodeName == 'LI' && e.target.remove();
})

```
## event bubbling
event bubbling occurs when a child eventListener is triggered along with all other eventListeners of the parents. Event triggers are propagated.
```js

	container.addEventListener('click', (e) => {
		e.stopPropagation(); // it stops event bubbling
	})

```

## callbacks
call stack is a mechanism used by the interpreter that is used to keep track of its place in the script that calls multiple functions
- when a script calls a function, that function is added to the stack
- any functions that are called by this function are added to the stack further
- when the current function is finished, that function is popped off of the stack

```js
//callbacks
setTimeout(() => {
	//statement
}, delay)
```

#### callback hell
this is when the script uses many nested callbacks making the code difficult to read
```js
function calls(delay, success, failure){

		let status = Math.floor((Math.random()*5000)+1);

		if(status > 3000){
				setTimeout(success(), delay);
		}
		else{
				setTimeout(failure(), delay);
		}
}

calls(2000, () => {
		console.log("Success (1)");
		calls(2000, () => {
				console.log("Success (2)");
		}, () => {
				console.log("failed (2)");
		})
},
		() => {
				console.log("failed (1)");
		}
)

```
## Promises
promises object represents the eventual completion (or failure) of an asynchronous operation and its resulting value.
- its an proxy for a value that is not yet known when the promise is created.
- using promises we can associate handlers with this yet to be known value
- promises can be in three states
	1. pending
	2. fulfilled
	3. rejected

```js
// creating a new promise
new Promise((resolve, reject) => { // resolve and reject are custom func names
	resolve(); //calling resolve() [the first arg func]	will fullful the promise
})
new Promise((resolve, reject) => { // resolve and reject are custom func names
	reject(); //calling reject() [the second arg func]	will reject the promise
})

//sample promise that waits for a random status code. If status is above 3000, it is fullfilled or else it is rejected.
new Promise((resolve, reject) => {
	let status = Math.floor(Math.random()*5000)+1;
	setTimeout(() => {
		if(status > 3000){
			resolve();
		}
		reject();
	},2000)
})

//managing promises
let getPage = (url) => {
	new Promise((resolve, reject) => {
		let status = Math.floor(Math.random()*5000)+1;
		setTimeout(() => {
			if(status > 3000){
				resolve(`Data from ${url}`);
			}
			reject(`Couldn't fetch ${url}`);
		},2000)
	})
}

getPage("nasa.org")
.then((data) => {
	console.log("Success (page 1)");
	console.log(data);
	return getPage("spacex.com"); // since we return a promise here, we can call .then next
})
.then((data) => { 
	console.log("Success (page 2)");
	console.log(data);
})
.catch((err) => {
	console.log("Failed..");
	console.log(err);
}) 
```
## Async functions
- these functions returns a promise
```js
let login = async (username, password){
	if(!username || !password) throw "missing creds"; // using throw will result in a rejected promise
	if(password === 'dew') return 'success'; // using return will result in a fulfilled promise
	throw 'invalid login';
}

login("asdf","add")
	.then(msg => {
		console.log("DONE LOGIN!");
		console.log(msg);
	})
	.catch(err => {
		console.log("ERRORd");
		console.log(err);
	})

//await keyword waits for an async function to finish up before moving to next line

function delayedColorChange(color, delay){
	//changes the body's backgroundColor value after 'delay' seconds.
}

async function colors(){
	await delayedColorChange('red',1000); // interpreter waits till completion
	await delayedColorChange('orange',1000);
	await delayedColorChange('yellow',1000);
	await delayedColorChange('green',1000);
	await delayedColorChange('blue',1000);
	await delayedColorChange('violet',1000);
	return "All good."
}
```
## error handling
```js
async function sample(){
	try{
		await someFunction();
	} catch(e){
		console.log("The error: ",e);
	}
}
```
## JSON - JavaScript Object Notation
- it is used in transfer of data
```js
let data = '';
jsonData = JSON.parse(data) // will convert the string to json data
jsonString = JSON.stringify(jsonData) // will convert a JSON data to string
```
### fetch api
```js
fetch(apiURL)
	.then(res => {
		return res.json(); //.json method returns a promise
	})
	.then(data => { //we can call another .then only because we return a promise in the above .then
		console.log(data)
	})
```
### axios
```js
config = {headers: {Accept: 'application/json'}};
axios.get(apiURL,config)
	.then(data => {
		console.log(data);
	})
	.catch(err => {
		console.log(err);
	})
```
## prototypes
- it contains all the common methods and function specific to that datatype. 
- objects of that datatype look upto the prototype methods under its datatype
```js
//to modify prototypes
Array.prototype.pop = () => {
	console.log('mod the pop behavior');
}
```
### factory functions
```js
function makeColor(r,g,b){
	const color = {};
	color.r = r;
	color.g = g;
	color.b = b;

	color.rgb = () => {
		const {r,g,b} = this;
		return `rgb(${r}, ${g}, ${b})`;
	}
}
```
### constructor function
```js
function Color(r,g,b){
	this.r = r;
	this.g = g;
	this.b = b;
}
//to add methods to the prototype for common access about all its objects
Color.prototype.rgb = () => {
	const {r,g,b} = this;
	return `rgb(${r}, ${g}, ${b})`
}

//to create objects
const color1 = new Color(45,67,23);
```
### class
```js
class Color(r,g,b){
	constructor(r,g,b){
		this.r = r;
		this.g = g;
		this.b = b;
	}
	rgb(){
		return `rgb(${r},${g},${b})`
	}
}
//creating objects
const c1 = new Color(34,45,55)

//inheritance
class Pet{
	constructor(name, age){
		this.name = name;
		this.age = age;
	}

	eat(){
		return `${name} is eating.`;
	}
}

class Dog extends Pet{
	bark(){
		return `${this.name}, the dog, is barking`
	}
}
class Cat extends Pet{
	constructor(name,age,lives = 9){
		super(name,age);
		this.livesLeft = lives;
	}
	bark(){
		return `${this.name}, the cat, is mewwwing`
	}
}
```
