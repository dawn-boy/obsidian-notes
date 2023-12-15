# datatypes
==Not like C, variables can store any datatype values;==
- number (All the numbers, decimals included are considered within this one category) [** is exponent.]
- string
- null
- boolean
- undefined - NaN (NaN stands for Not a Number, but it's considered within the number datatype. ==Those javascript memes are beginning to make sense..==)

# declaring 
```js
let num = 3;
const speedOfLight = 299792458; // constant, cannot change
let isCap = true, isCap = false;

// old way of doing things
var num = 3;
```

# string methods
```js
let string = "HelloThere";

string.toUpperCase();
string.toLowerCase();
string.trim();
string.indexOf(wordToSearch);
string.slice(startIndex, endIndex);
string.replace(whatToReplace, whatToReplaceWith); //replaces only the first occ
string.repeat(timesToRepeat)

//formated string

let genName = "Kenobi";
"Hello There! general ${genName}";


```
