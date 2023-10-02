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
