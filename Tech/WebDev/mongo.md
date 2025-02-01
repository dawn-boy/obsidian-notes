```js
//database
use db
db
show dbs

//collections
show collections
db.collectionName.drop()

//to insert into database
db.dogs.insert({key: value})
db.dogs.insert([{key1: val1},{key2:val2}])

//to find
db.dogs.find() //returns all data
db.dogs.find({key: value})
db.dogs.findOne({key: value})
db.dogs.findOne({'something.key': val})
db.dogs.find({key: {$gt: 4}}) //conditions
db.dogs.find({key: {$in: [val1, val2]}})
db.dogs.find({key: {$or: [condition1, condition2]}})

//to update
db.dogs.updateOne({find: val}, {$set: {key1: val1, key2: val2}})

//to delele
db.dogs.deleteOne({key: val}) //deletes the first match
db.dogs.deleteMany({key: val}) //deletes every match
db.dogs.deleteMany({})
```
## mongoose 
```js
// npm i mongoose
const mongoose = require('mongoose');
mongoose.connect('mongodb://localhost:27017/movieApp',{ useNewUrlParser: true });
	.then(() => {
		console.log("Connection success");
	})
	.catch((err) => {
		console.log("oh no error");
		console.log(err);
	})
```
#### to create a movie schema
```js
const movieSchema = new mongoose.Schema({
	title: String,
	year: {
		type: Number,
		required: true,
		maxlength: 20
	},
	score: {
		type: Number,
		min: 0
	},
	rating: {
		enum: ['R', 'PG-13', 'U', 'PG-12']
	},
	cast: [String],
	awards: {
		oscars: {
			type: Number,
			defaults: 0
		},
		emmys: {
			type: Number,
			defaults: 0
		}
	},
	
});

//instance methods
movieSchema.methods.methodName = function() {
	console.log(`The ${this.title} has a score of ${this.score}. It has won ${this.awards.oscars} oscars and ${this.awards.emmys} Emmys, all the while being a ${rating}-rated Movie!!`)	
}
//static methods
movieSchema.static.methodName = function() {
	//statements
}
//property getter and setter functions for the given property name
movieSchema.virual('propertyName')
	.get(function(){
		//statements
	}) 
	.set(function(){
		//statements	
	})

//middleware
movieSchema.pre('save', async function(){
	//statements
})
movieSchema.post('save', async function(){
	//statements
})

const Movie = mongoose.model('Movie', movieSchema); //.model() returns a class. 'Movie' argument needs to have first letter capital and a singular word. Mongoose creates a collection called movies with this.
const jurassicPark = new Movie({title: "Jurassic Park", year: 1988, score: 10, rating: "The Best"});


//changing values
jurassicPark.score = 100;
jurassicPark.save(); //returns  a promise. saves locally to the mongo collection



//insert many
// this takes time so a promise is returned
Movie.insertMany([
{keys:vals},
{keys:vals},
{keys:vals},
{keys:vals}
])
	.then((data) => {
		console.log(data);
	});

//to find movie
// returns a query, not a promise. Queries are nearly like promises.
//queries are returned because searching takes time.
Movie.find()
	.then(data => console.log(data)); // we can stack up then with a query

Movie.findById(id)
	.then(data => console.log(data)); // searches by id 

Movie.find({rating: 'R'})
	.then(data => console.log(data));

Movie.findOne({rating: 'R'})
	.then(data => console.log(data));

Movie.findOne({rating: 'R'}).exec() //gives a fully-fledged promise
	.then(data => console.log(data));

//to update movie
//returns a thennable object, but only its status not the data itself
Movie.updateOne({title: 'Amadeus'}, {year: 1999})
	.then(res => console.log(res));

Movie.updateMany({title: {$in: ['Amadeus', 'Stand by me']}},{year: 2000})
	 .then(res => console.log(res));

Movie.delete({year: {$gte: 10}})
	.then(res => console.log(res));

//returns the data
//new option will return the modified object data
//runValidators option will check the schema for restrictions and throw errors if input doesn't agree with them
Movie.findOneAndUpdate({title: 'Greece'}, {score: 10}, {new: true, runValidators: true})
	.then(data => console.log(data)); 

//using await and async
app.get('product', async ( req,res ) => {
	const products = await Product.find( {} );
	console.log(products);
})
```