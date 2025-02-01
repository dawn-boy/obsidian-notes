## Node.js
- its a javascript runtime environment that comes in without the browser side stuffs like window, document, DOM apis, etc.
- but it comes with lot of other built-in modules that helps in interacting with the operation system
```js
const args = process.argv.slice(2); //first two elements are the filename and path

for(let arg of args){
	console.log(arg);
}

const name = process.argv[2] || "DefaultVal"

```
## file operations
```js
const fs = require('fs');

try{
	fs.mkdirSync('cat'); //synchronous
	fs.mkdir();
	
	fs.writeFileSync(name)
} catch(e){
	console.log("Something");
}
```
## module exports
```js
//to create our very own moduels for importing in java
//create a new file and put these contents
module.exports.add = (x,y) => x+y; //module.exports prefix is needed 
module.exports.PI = 3.1409843957467
// either all that or

add = (x,y) => x+y;
PI = 3.4534;

mod = {add: add, PI: PI};
module.exports = mod;

//short-form
exports.add = (x,y) => x+y;
exports.PI = 3.14234;

//in out main.js file
const mod = require('./fileName');

//to create a index.js for an entire directory (mods) full of modules
// inside index.js

const mod1 = require('./mod1');
const mod2 = require('./mod2');
const mod3 = require('./mod3');

exports = [mod1, mod2, mod3];

//inside main.js
const mods = require('./mods');
```
## npm
```js
npm install package-name

//inside the file.js
const mod = require('mod');

//to use a tool within file.js
npm link toolName //like npm link cowsay

//to keep track of all the modules installed for the app.js
npm init
npm i package-name
```
## express

```js
//installation
npm i express

//usage
const express = require('express');
const app = express();

app.use( (req,res) => {
	console.log("We have a new request!");
	res.send('<h1>Hello, this is my webpage</h1>');
	res.send({color: 'green'});
})

//static files
app.use(express.static(path.join(__dirname, 'public'))); //need to have a public directory inside the project folder.
//can access those static files using /fileName

app.listen(8080, () => {
	console.log("Listening on port 8080);
}) 

//routing 

//get requests
app.get('/', (req, res) => {
	res.send("This is the home page");
})
app.get('/about', (req, res) => {
	res.send("This is the about page");
})
app.get('/contact', (req, res) => {
	res.get("This is the contact page");
})

//post requests
app.post('/cats', (req, res) => {
	res.get("Something");
})

//path params
app.get('/r/:subreddit', (req, res) => {
	const { subreddit } = req.params;
	res.send(`Accessing the ${subreddit} subreddit`);
})
```
## view engine
- make a directory called views. This is the default location express searches for .ejs files
- inside the render function, don't have to pass in the views/ prefix, as it has a default lookout
```js
const path = require('path');

app.set('view engine', 'ejs');
//to make the views dir path absolute, instead of its default relative addressing
app.set('views', path.join(__dirname,'/views'))
app.get('/', (req, res) => {
	res.render('fileName.ejs');
	}
);
```
## ejs
```js
app.get('/rand', (res, req) => {
	const num = Math.floor(Math.random() * 10) + 1;
	res.render('home', { rand: num });
})
```

inside the home.ejs file inside the /views directory
```html
<html>
	<head>
		<!-- accessing a static .css file --> 
		<link href="/fileName" rel='stylesheet'> 
	</head>
	<body>

		<!-- we use the = here to indicate that it is to be rendered -->
		<%= rand %>	

		<!-- without the =, code will be executed but not rendered. -->

		<!-- conditionals --> 
		<% if(condition) { %> 
			<%= var %>
			<h1> THis will be displayed </h1>
		<% } else { %>
			<h1> This h1 will be displayed </h1>
		<% } %>

		<!-- for loop -->
		<ul>
			<% for(let search of history) { %>
				<li> <%= search %> </li>
			<% } %>
		</ul>

	</body>
</html>
```
#### partials
```html
<!-- if there's a recurring code in the .ejs files, we can copy the redundant code to a common file from where other files access it -->

<!-- copy redundant code to partials/common.ejs -->

<!-- inside other files -->
<%- include('partials/head') %>
<body>

<%- include('partials/navBar') %>
.
.
.
</body>
</html>
```
### parsing form data
```js
// for parsing form data
app.use(express.urlencoded( { extended: true } ))
// for parsing json data
app.use(express.json())

app.post('/tacos', ( req, res ) => {
	const { data1, data2 } = req.body;
})
```
## get vs post requests
### Get requests
- used to retrieve data
- data is sent via a query string
- information is plainly visible in the url
- only limited amount of data can be sent
### Post requests
- used to post data to the servers
- used to write/create/update data to the servers
- data is sent via the request body, not as a query string
- it can send any type of data, like JSON.
## uuid 
#### (universally unique identifier)
```js
//npm i uuid

const { v4: uuid } = require('uuid');
uuid(); //returns a unique identifier
```
## CRUD functionality 
#### (Create Read Update Delete)
##### a basic format for a commenting website
- (Index route) GET /comments -> to get all the comments
	- an All comment page
- (Create route) POST /comments -> to create a new comment
	- a form page and redirection to index page
- (Show route) GET /comments/:id -> to get a specific comment
	- a specific comment page
- (Update route) PATCH /comments/:id -> to update a specific comment
	- 
- (Destroy route) DELETE /comments/:id -> to delete a specific comment

```html
<!-- /comment/edit.ejs -->
<form method='post' action='/comments/<%= comment.id %>?_method=PATCH'>
	<textarea name='comment' cols='30' rows='10'>
		<%= comment.comment %>
	</textarea>
	<button> Save </button>
</form>
<!-- end of /comment/edit.ejs -->

<!-- /comment/show.ejs -->
<body>
	<form method='post' action='/comments/<%= commend.id %>?_method=DELETE'>
		<button>Delete</button>
	<form>
</body>
<!-- end of /comment/show.ejs -->
```

```js
//npm i method-override
//so we can trick forms into giving a PATCH request because it can't give anything else other than POST and GET
const methodOverride = require('method-override');
app.use(methodOverrid('_method'))

let comments = [{
	id: uuid(),
	user: name,
	comment: something
}];

//the path /comments/* is located inside __dirname/views/ 

//index route
app.get('/comments', ( req, res ) => {
	res.render('/comments/index', { comments })	
})

//create route
app.post('/comments', ( req, res ) => {
	const { user, comment } = req.body;
	comments.push({ id: uuid(), user, comment });
	res.redirect('/comments');
})

//show route
app.get('/comments/:id', ( req, res ) => {
	const id = req.param;
	const comment = comments.find(c => c.id === id);
	res.render('comment/show', ...comment);
})

//update route
app.get('/comments/:id/edit', ( req, res ) => {
	const { id } = req.params;
	const foundComment = comments.find( c => c.id === id );
	res.render('/comment/edit', { comment: foundComment });-
})
app.patch('/comments/:id', ( req, res ) => {
	const { id } = req.params;
	const newComment = req.body.comment;
	const foundComment = comments.find(c => c.id === id );
	foundComment.comment = newComment;
	res.redirect('/comments');
})

//delete route
app.delete('/comments/:id', ( req, res ) => {
	const { id } = req.params;
	comments = comments.filter(c => c !== c.id );
	res.redirect('/comments');
})
```