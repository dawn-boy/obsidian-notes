## middleware
- middleware are just functions that has access to the request and response objects
- they can end a request-response cycle
- they have access to the next middleware function. Usually the next middleware functions are called "next"
## fake login using middleware
==if the user manually types in the route.. this middleware authentication fails.==
```js
const verifyLogin = ( req, res, next ) => {
	const { username, password } = req.query;
	if ( username == 'something' && password == 'something' ){
		next();
	}
	res.send("nope");
}

app.get( '/', verifyLogin, ( req, res ) => {
	res.render( 'root' );
} )
```
## errors
```js
// to throw an error
throw new Error("Password required")

// at the end
app.use(( err, req, res, next )){
	console.log("Errored")	
	console.log(err)
	next(err);
}

```

