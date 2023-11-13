- Cascading Style Sheets
it's called Cascading, so the style that's closer to the end of the sheet will always take precedence
Order of Precedence: 
	- ID Selectors,
	- Class Selectors,
	- Element Selectors.
# comments
```css
/* this is a comment */
```
# basic syntax
```css
selector {
	property: value or none;
}
```

# text properties
```css
text-align: center;
font-weight: bold;
text-decoration: blue underline wavy;
line-height: 2;
letter-spacing: 15px;
font-size: 10px;
font-family: sans-serif helvetica cursive;
```

# Selectors
```css
* {
/* this is the universal selector */
}

img {
/* this is an element selector */
}

h1, h2 {
/* this groups the selectors and applies the styles to them all */
}

#search {
/* this is an id selector */
}

.tag {
/* this is a class selector */
}

/* Descendent Selector */

li a {
/* this is a descendent selector, here it selects all <a> tags within all <li> tags. No <li> tags will be styled here, only those <a> that are nested inside <li> tags */
}

#search a {
/* this is a descendent selector acting on <a> tags within the tags containing id='search' */
}

/* Adjacent Selector */

p + a {
/* selects all the <a> tags that are right after <p> tags *
}

/* Direct Child Selector */

p > a {
/* This selects all the <a> tags that are direct descendent of <p> tags*
}

/* Attribute Selector */

input[type='text'] {
/* Selects all the <input type="text"> tags */
}

```

# Pseudo Classes
```css
a:hover {
/* Apply these styles when cursor hovers */
}
a:active {
/* apply these styles when the link is clicked */
}
section:nth-of-type(2n){
/* apply these styles to all the even number sections */
}
```

# Pseudo Selectors
```css
a::first-letter{}
a::first-line{}
```

# CSS Box Model
### Padding
This is the space between the content box and the border. 

```css
div {
	padding: 10px;
	padding: 40px 50px 20px 30px;
}
```
### Border
This is the border surrounding the content box.

```css
div {
	border-width: 20px;
	border-left-width: 10px;
	
	border-color: blue;
	border-left-color: darkblue;

	border-style: dashed;
	border-left-style: dotted;

	border: width style color;

	box-sizing: border-box; /* This won't add any additional width to the content box */

	border-radius: 20px 20px 20px 20px;

}
```
### Margin
This is the space between two box models.

```css
div {
	margin: 10px;
	margin: 10px 30px 40px 20px;
}
```
## Content Box
**Width** and **Height** control this content box
```css
div {
	width: 100px;
	height: 100px;
}
```

# Display
```css
div {
	display: inline;
	display: block;
	display: inline-block;
}
```
- inline
Inline elements don't push the next elements down, they adjust and fit in with the next element, taking just the needed space.

**Width and Height properties are ignored.**
**Padding works but is ignored by other elements**
**Margin is only respected within that line**
 
- block
Block elements takes the entire line for themselves, even when the content box doesn't use all that space.

**Width and Height properties are respected**
**Padding is also respected**
**Margin is also respected everywhere**

- inline-block
Inline-block elements behave as inline elements but they respect those properties that inline don't, like, Height and width, padding and margin, etc.

# Units
## percentages
relative to the parent
## em
gets the initial size value from the parent, then it's all other properties scaled with em are relative to the element itself. 
```html
<ul>
	<li>element1</li>
		<ul>
			<li>element1.1</li>
			<li>element1.2</li>
		</ul>
	<li>element2</li>
		<ul>
			<li>element2.1</li>
			<li>elememt2.2</li>
		</ul>
</ul>
```
```css
ul {
	font-size: 1.5em
}
```
### Shortcomings of em
in here, em causes the nested lists to inherit their parent's size and size itself accordinngly, so now this has an undesired effect like as you go through each nested list, the list elements size decreases or increases.

## rem
gets the root html's size value, and this doesn't change wherever you are in that document.

# position
```css
div {
	position: static;
	position: relative;
	position: absolute;
	position: fixed; 
	/* stays on the given postion even when the screen is scrolled */
	position: sticky;
	/* stays on the given postion when the screen is scrolled and when it hits the top */

	top: 10px;
	left: 10px;
	bottom: 10px;
	right: 10px;
}
```
# transition
```css
div{
	background-color: red;
}
div:hover {
	background-color: deepblue;
	transition: background-color 3s ease-in 1s;
	/* Propery Name | Transition  speed | Timing function | Delay */
}
```
# transform
```css
div{
	transform-origin: bottom right;
	transform: rotate(45deg);
	transform: rotateX(180deg);

	transform: scale(0.5 2);
	/* Height | Width */

	transform: translate(10px);
	
}
```
# background-image
```css
div{
	background-image: url(url_to_the_image)
	background-size: cover;
}
```

***
# Flex

flex helps us to space the elements inside a container however we want.
```css

/* The Main axis is the horizontal one, The Cross axis is the vertical one */

div {
	/* This turns it on. */
	display: flex;

	flex-direction: row;
	flex-direction: row-reverse;
	flex-direction: column;
	flex-direction: column-reverse;

	justify-content: flex-start;
	justify-content: flex-end;
	justify-content: center;
	justify-content: space-between;
	justify-content: space-around;
	justify-content: space-evenly;

	flex-wrap: nowrap;
	flex-wrap: wrap;
	flex-wrap: wrap-reverse;

	align-items: center;
	align-items: flex-start;
	align-items: flex-end;

	/* For Individual elements */
	align-self: flex-start;
	align-content: flex-start;

	flex-basis: 400px;
}
```

## Media Queries
```css
@media (width: 400px){
	div{
		color: blue;
	}
@media (min-width: 400px){
	div{
		color: pink;
	}
}
}
```
---
# Flex
```css

/* Initiates Flex Protocols */
display: flex;

/* If the Screen shrinks, then the contents will either shrink with it or just go past the border */
flex-shrink: 1;
/*Allowed to grow and fill the screen if the value is 1 */
flex-grow: 1;

/* Wraps the elements one below another when the screen size gets smaller */
flex-wrap: wrap;

```