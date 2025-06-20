# It's more about telling what to do rather than how to do it. That's React!
React is a library for building user interfaces by splitting the interface into re-usable components.

***
# JSX (Javascript XML)
- JSX allows for HTML-like code to be written within javascript

```jsx
function Component(){
	return <div>Hello world</div>
}

function Component2(){
	return (
		<div>
			<div>Hii</div>
			<div>Hello</div>
		</div>
	)
}

function Component3(){
	return (
		<>
			<div>Heehe</div>
			<div>Nice to meet ya!</div>
		</>
	)
}
```
- every `return` statement can only return a single DOM element. 
- if we need to return multiple DOM elements without adding in another `<div>` element, we can use ***React Fragments!!***
	- React Fragments => `<>` and `</>`
	- they keep the DOM clean without any unnecessary wrappers.

```jsx
function Component(){
	return <div className="App">Hi again</div>
}
```
- since the keyword `class` is reserved in Javascript Object Oriented programming, we use `className` to denote a element's class

```jsx
function Component(){
	return (
		<div>
			{value === 0} is the answer.
		</div>
	)
}
```
- if there's any need for Javascript expressions within the HTML codes, we can use `{}`

***
# Elements and Components
## Elements
They are the smallest building blocks in React. Elements are Immutable meaning they cannot be changed after creation
## Syntax
```jsx
const element = <h1>Out beyond ideas of wrongdoing and rightdoing, there is a field. I'll meet you there.</h1>
```
## Components
These are re-useable functions that return JSX code.
### Syntax
```jsx
function Quote({ props }){
	return <h1>When the soul lies down in that grass.</h1>
}
```
## Props (Properties)
Props are read-only data passed from parent to child components. Components receive them as parameters.
### Component definition
```jsx
function Quote(props){
	return <h1>{props.author} - The World is too full of talk about.</h1>
}
```

- or we can destruct the props as we get them
```jsx
function Quote({ author }){
	return <h1>{author} - The world is too full of talk about.</h1>
}
```
### Component usage
```jsx
<Quote author="Rumi" />
```

***
# Rendering in React
we can control what gets to be on the screen based on conditions. The most common types I've used are

## 1. Ternary Operators
when we have two options and want a simple switch
### Syntax
```jsx
{ Boolvariable ? TrueLogic : FalseLogic }
```
### Example
```jsx
{ isLoggedIn ? <Welcome /> : <Login />}
```

## 2. Logical AND
when we want to render a component only if the given boolean variable is `true`
### Syntax
```jsx
{ BoolVariable && Component }
```
### Example
```jsx
{ isAdmin && <AdminPanel /> }
```

## 3. if / else statements
if there's a need for a more complex logic 
### Syntax
```jsx
{
	if(BoolVariable){
		return thisLogic
	}
	return thatLogic
}
```
### Example
```jsx
{
	if(LoggedIn){
		if(isAdmin){
			return <h1>Great You're here now</h1>
		}
		return <h1>oh.. you're back :|</h1>
	}
	return <h1>Not Logged in</h1>
	
}
```
## 4. Switch cases
if that logic is to be based on a single variable with changing values and also that logic is complex, Switch is the perfect saviour!
### Syntax
```jsx
switch (Variable){
	case value1:
		return thisLogic
	case value2:
		return thatLogic
	case value3:
		return someLogic
	default: 
		return TheLogic
}
```
- since we use return here inside the `case`, we don't have to explicitly `break` every time
### Example
```jsx
switch (status) {
	case 'loading':
		return <LoadingSpinner />;
	case 'success':
		return <SuccessMessage />;
	case 'error':
		return <ErrorMessage />;
	default:
		return null;
}
```
## 5. Rendering a list of items
If we have a list of items that we need to recursively render on the page, then Javascript's `.map()` comes to the rescue.
### Syntax
```jsx
{
	iterable.map(element => {
		<Component key=SomeUniqVal data={element}
	})
}
```
### Example
- here's the object file 
```js
items = [
	{
		id: 0,
		name: "kat"
	},
	{
		id: 1,
		name: "benie"
	}
]
```

- and inside a component we are rendering it recursively
```jsx
{
	items.map(tempvar => {
		<Item key={item.id}	data={item} />
	})
}
```

***
# Hooks
These hooks allow functional components do more than just be pure functions. They essentially lets us hook into more react functionality.
## but what's a pure function?
It's a function that returns the ***same output for the same input*** and has ***no side-effects***.
## but what's a side-effect?
It's an operation that affects the outside world or depends on it.
## Example
- This is a pure function, same input => same output
```js
function add(a,b){
	return a + b;
}
```

- This is an impure function, 
```js
let total = 7
function summation(num){
	total += num;
	return total;
}
```
- output depends on an external variable `total`.
- it also modifies ***an external value*** => ***giving side-effects*** => ***making it impure***
## We have many hooks in React!
### **1. useState()**
- it essentially a variable that **react keeps track** of and **whenever there's a change** any component that uses it will be **re-rendered** to display the current value.
- it return `[state, setState]` 
	- `state` => a state (variable) where our value is stored.
	- `setState` => a setter function for that state. ***==Do not mutate the state directly, react will not track those changes. Always use the setter function.==***
#### Syntax
```jsx
const [state, setState] = useState(initialValue);
```
#### Example
```jsx
const [count, setCount] = useState(0);
```
### **2. useEffect()**
- we use this to run our side-effects, like fetching data, updating DOM elements, etc.
- useEffect runs after only after a component renders, so it has access to those DOM elements.
- It takes in a dependency array of variables, which it keep track of. Whenever there's a change, the effect runs again!
#### Syntax
```jsx
useEffect( function(), [dependency array] );
```
#### Example
```jsx
let quote = "What you seek is seeking you."

useEffect( () => {
	console.log(quote)
	
	return () => {
		console.log("This is a cleanup function")
	}	
	
}, [ quote ])
```
- so whenever there's a change in the quote, we will run the useEffect.
- The cleanup function runs only when the component un-mounts meaning when the component is not rendered then the cleanup function kicks in.
### ***3. useRef()***
- It is used to **store mutable values** that **doesn't cause re-renders** but **persists for the full lifetime** of the component, unlike the regular variables
- we commonly use this hook to reference DOM elements
#### How we connect DOM elements to useRef?
```jsx
const inputElem = useRef(null);
<input ref={inputElem} />
```
#### Storing normal values
```jsx
const countRef = useRef(0)
// mutation
countRef.current = 6;
// displaying
<div>{countRef.current}</div>
```
### **4. useReducer()**
- An Upgrade to `useState()` hook. 
- `useReducer()` intends to give you **a centralized control** for **managing multiple states** with **complex state logic**.
#### Syntax
```jsx
const reducer = (state, action) => {
	some state managing logic;
}

const initialValues = {
	stateOne: 0,
	stateTwo: 0,
}

const [state, dispatch] = useReducer(reducer, initialValues)
```
- The `reducer()` function takes in `(state, action)` parameters,
	- `state` => gives the current value of all the state variables. 
		In this example, `reducer()` gets  `stateOne` and `stateTwo` current values. we can access them by 
		`state.stateOne` or `state.stateTwo`
	- `action` => the current action perform. Passed through the `dispatch(action)` 
- the `initialValues` object has the initial values for all the states we'll be using 
- `useReducer()` returns `[state, dispatch]` 
	- with `state`, we can access the current state value, like `state.stateOne` and `state.stateTwo`
	- with `dispatch()`, we can pass in actions to the `reducer()` logic
#### Example
```js
import { useReducer } from 'react';

function Component(){

	function reducer(state, action){
		switch(action.type){
			case 'increment':
				return { count: state.count + 1 };
			case 'decrement':
				return { count: state.count - 1 };
			case 'reset': 
				return { count: 0 };
			default:
				return state;
		}
	}
	
	const initialValues = {
		count: 10
	}
	
	const [state, dispatch] = useReducer(reducer, initiatValues)

	return (
		<h1> The Count is {state.count}</h1>
		<button
			onClick={ () => {
				dispatch({ type: 'increment' })
			}}
		/> + </button>
		<button
			onClick={ () => {
				dispatch({ type: 'decrement' })
			}}
		/> - </button>
		<button
			onClick={ () => {
				dispatch({ type: 'reset' })
			}}
		/> RESET </button>
	)
}
```
## `Regular variable` vs `States` vs `Refs`

| Features             | Variables                | States                                | Refs                                                                 |
| -------------------- | ------------------------ | ------------------------------------- | -------------------------------------------------------------------- |
| Survives re-renders? | Nope                     | Yep                                   | Yep                                                                  |
| Triggers re-renders? | Nope                     | Yep                                   | Nope                                                                 |
| Mutable              | Yep (direct mutation)    | Yep(setter function)                  | Yep (using .current)                                                 |
| When to use?         | To store temporary logic | to store data that changes UI         | to store something across re-renders but doesn't trigger re-renders  |
