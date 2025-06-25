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
==*Every Variables that is used within the `useEffect` function logic must go inside the dependency array**Not Doing so would lead to Stale Closure**==
#### What is Stale Closure?
Stale closure occurs when the useEffect references outdated states or props.
##### Example
```jsx
useEffect(() => {
	document.title = `You have ${count} items`;
},[])
```
- since count is not included within the dependency array, this is a stale closure
- when count updates to a new value, this hook will still be referencing the old one. YAY!

==But keep in mind about the reference value types. Even if you update an object with a same value as before, it still triggers a re-render because the references change.==

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

| Features             | Variables                | States                        | Refs                                                                |
| -------------------- | ------------------------ | ----------------------------- | ------------------------------------------------------------------- |
| Survives re-renders? | Nope                     | Yep                           | Yep                                                                 |
| Triggers re-renders? | Nope                     | Yep                           | Nope                                                                |
| Mutable              | Yep (direct mutation)    | Yep(setter function)          | Yep (using .current)                                                |
| When to use?         | To store temporary logic | to store data that changes UI | to store something across re-renders but doesn't trigger re-renders |
# 5. [[#useContext hook]]
***
### the progress bar?
Just a useful bar that shows the progress.
```jsx
<progress max={value} value={someVal} />
```
# Styles within jsx

in the css file
```css
.main{
	/* all the styles here */
}
```

in the jsx file
```jsx
import styles from "./Component.module.css"

export default function Component(){
	return (
		<main className={styles.main}>
		</main>
	)
}
```
***
# React-Router-dom
 ## Single Page Applications
 
Basic import and setup
```jsx
import { BrowserRouter, Routes, Route } from 'react-router-dom';

function App(){
	return(
			<BrowserRouter>
				<Routes>
					<Route path='login' element={<Login />} />
					<Route path='signup' element={<SignUp />} />
					<Route path='*' element={<PageNotFound />} />
				</Routes>
			</BrowserRouter>	
	)
}
```

- Nested Routes can be created by
```jsx
import { Outlet } from 'react-router-dom'

<Route path='app' element={<App />}>
	<Route path='dev' element={<p>THis is a dev</p>} />
	<Route path='build' element={<p>THis is a build </p>} />
	// include an index route if there's no match from child routes
	<Route index element={<HomePage />} />
</Route>

// inside the <App />
function App(){
	//all code here
	<Outlet />
	//all code here
}
```
- the children routes specify what component to display using the `element` property
- the `<Outlet />` specifies where to display that component

To move between pages
```jsx
// THe wrong way
<a href="/login"> Login </a>

// The Right way
import { Link } from 'react-router-dom'
<Link to="/login"> Login </Link>

// for nested routes globally
<Link to="/app/login"> Login </Link>
```
- using the anchor tag would do a hard page refresh which isn't optimal. 
- The `Link` component from the `react-router-dom` library changes only the DOM element not the whole page

For NavBar links, `react-router-dom` gives us `<NavLink />`. It just adds upon the basic `<Link />` with `className = 'active'`  for the currently selected page.
```jsx
import { NavLink } from 'react-router-dom';
<NavLink to='/login'> Login </NavLink>
```
## To Store data within the URL

- Let's say we have a component called `<City />`
```jsx
import { Link } from 'react-router-dom'

export default function City(){
	// Lots of map related code
	
	<Link to={`/countries/cities/${id}`}>MayBel</Link>
}
```
- so basically, it just re-routes to `Maybel`'s id when we click it,

- now, we defined that path using `<Route>`
```jsx
export default function App(){
	<BrowserRouter>
		<Routes>
			<Route ... />
			
			<Route path='/countries' ...>
				<Route ... />
				<Route path='cities/:id' element={<City />} />
				<Route ... />
			</Route>
			
		</Routes>
	</BrowserRouter>
}
```

- To use the params from the URL within `<City />` component
```jsx
import { useParams } from 'react-router-dom'

const { id } = useParams();
```

- To use searchParams from the url
```jsx 
import { useSearchParams } from 'react-router-dom'

const [searchParams, setSearchParams] = useSearchParams();

const lat = searchParams.get('lat')
const lng = searchParams.get('lng')

// to change
setStateParams({ lat: ..., lng: ...})
```

# `useNavigate()` function

## The Imperative approach
### If we want to navigate to the child routes without `<Link />` or `<NavLink />`
```jsx
import { useNavigate } from 'react-router-dom'

const navigate = useNavigate()

<div onClick={() => navigate('/cities', { replace: true})} />
```
## The Declarative approach
```jsx
import { Navigate } from 'react-router-dom'

<Navigate replace to="/cities" />
```
- `replace` keyword to make back button functional. 

***
# Context API
we have the problem of Props drilling, passing a prop to all the intermediary components just so we can have it to a children element.
- Context API makes a widely used state globally available to all the components lest there be props drilling

## useContext hook
1. Create a context
```jsx
import { createContext } from 'react';

const newContext = createContext();
```

2. Providing access to components
```jsx
<newContext.Provider value={ name: "adithya" }>
	<App />
</newContext.Provider>
```

3. Use the context within the components
```jsx
import { useContext } from 'react';

function App(){
	const context = useContext(newContext);
	
	return <div>Hello {context.name}</div>
}
```
### A Better approach
It would look a lot cleaner if we've used a wrapper component

1. Create a separate `MyContext.js` file
```jsx
import { useContext, createContext, useState } from 'react';

// Create Context
const MyContext = createContext();

// Create a Provider component
function MyProvider({ children }){
	const [name, setName] = useState("Adhi");

	return(
		<MyContext.Provider value={{ name,setName }}>
			{ children }
		</MyContext.Provider>
	)
}

// this function keeps our context private
function useName(){
	const context = useContext(MyContext);
	return context;
}

export { useName, MyProvider }
```

2. Within the `App.jsx` file
```jsx
import { MyProvider } from './contexts/MyContext.js'
import Page from './components/page.js'

function App(){
	<MyProvider>
		<Page />
	</MyProvider>
}

export default App;
```

3. Inside the child `<Page />` Component
```jsx
import { useContext } from 'react';
import { MyContext } from '../contexts/MyContext.js'

export function Page(){
	const { name, setName } = useContext(MyContext);
	
	// more of your logic <3
}
```

***
# Authentication
We'll be using the Context API to achieve this

- `./contexts/AuthContext.js`
```jsx
import { createContext, useContext, useReducer } from 'react'

const AuthContext = createContext();

const initialValues = {
	user: null,
	isAuthenticated: false,
}
function reducer(state, action){
	switch(action.type){
		case 'login':
			return {
				...state,
				user: action.payload,
				isAuthenticated: true
			}
		case 'logout':
			return {
				...state,
				user: null,
				isAuthenticated: false,
			}
	}
}

const FAKE_USER = {
	name: "maybel",
	username: "duncun",
	password: "12345678",
	profile: 'https://cloud.google.com/hi.jpg'
}

function AuthProvider({ children }){

	const [{ user, isAuthenticated }, dispatch] = useReducer(reducer, intitialValues)

	function login(username, password){
		if(username === FAKE_USER.username && password === FAKE_USER.password) dispatch({ type: "login", payload: FAKE_USER })
	}
	function logout(){
	dispatch({ type: 'logout' })
	}

	return ( 
		<AuthContext.Provider value={{ user, isAuthenticated, login, logout }}>
			{ children }
		</AuthContext.Provider>
	)
}

function useAuth(){
	const auth = useContext(AuthContext);
	if(auth === undefined) throw new Error("Someone tried to access AuthContext outside the AuthProvider!")
	return auth;
}

export { AuthProvider, useAuth };
```

- To protect the routes that are only available to users
```jsx
import { useAuth } from './AuthProvider.js';
import { useNavigate } from 'react';

export function ProtectedRoute({ children }){
	const { isAuthenticated } = useAuth();
	const navigate = useNavigate();

	useEffect(function(){
		if(!isAuthenticated) 
			navigate('/homePage', { replace: true })
	},[navigate, isAuthenticated])

	return children
}
```

- in `App.jsx`
```jsx
import { AuthProvider } from './contexts/AuthProvider.js'
import { ProtectedRoute } from './contexts/ProtectedRoute.js'

function App(){
		<HomePage/>
		<AboutUs/>
		<AuthProvider>
			<ProtectedRoute>
				<DashBoard />
			</ProtectedRoute>
		</AuthProvider>
}
```

***
# Optimizing React Apps

we need to set somethings right, before we begin learning how to optimize apps.
## When does a component gets re-rendered?
only in these 3 scenarios,
1. At state updates
2. At a context change
3. At a Parent re-render
## What is a render?
A render is when the component function gets called. It is an expensive action so we must try to reduce it wherever we can.
## what is a wasted render?
Its a render that doesn't produce any changes in the DOM
- Not really a problem, because React is fast but when it happens too frequently, then things get outta hand.

## 1. Performance optimization with `{ children }`
### Scenario
- Say we have a component called `Test` that
	1. contains a state
	2. houses a slow component that doesn't depend on the state ( takes a long time to render )
so every time the state updates, `Test` re-renders, we also have our slow component re-rendering. 
===**So we pass in the slow component as a children**===
### Example
- This is our current code
```jsx
function Test(){
	const [count, setCount] = setState(0);

	return(
		//some code
		<SlowComponent />
	)
}
```

- Our optimized code
```jsx
function Test({ children }){
	const [count, setCount] = setState(0);

	return(
		//some code
		{ children }
	)
}
```

inside our `App.jsx`
```jsx
function App(){
	<Test>
		<SlowComponent />
	</Test>
}
```
## Why tho?
children elements are rendered outside the `<Test />` component and so when there's a state change within, the `<Test />` component just reuses the already created element passed via `{ children }`
## 2. Memoization
==**This'll work only for pure functions**==
The idea is that we cache the resulting data for their respective inputs. If these inputs are encountered again, we'll just use the cache data instead of recalculating the whole thing

we can memoize 
- components with `memo`
- objects with `useMemo`
- functions with `useCallback` 

Use memo only if we have a component that is big and re-renders frequently.

1. `memo` - Memoizing Components
```jsx
import { memo } from 'react';

const Memoed = memo(
	function Component(){
		//body
	}
)
```
- we have memoized the `<Component />` but even now it might still get re-rendered because
	there was a new object or function passed as prop each time the parent re-rendered.
### Example
```jsx
function App(){
	const archiveProps = { title: 'Post' };
	
	<Archive archiveProps={archiveProps} />
}

// or with a function

function App(){
	function something(){}
	
	<Archive something={something} />
}
```
Since objects and functions are reference types, each re-render from the parent creates a new reference and `memo` sees them as a **new prop => triggers re-render!**

==So, we memoize those objects and functions too :) simple==

2. `useMemo` - Memoizing values 
```jsx
function App(){

	const archiveProps = useMemo(() => {
		return { title: 'Props' }
	}, [])

	<Archive archiveProps={archiveProps} />
}
```

- if the object was dependent on an external variable
```jsx
function App(){

	const archiveProps = useMemo(() => {
		return { title: `Props - ${name}` }
	}, [name])

	<Archive archiveProps={archiveProps} />
}
```

 - if its a function
```jsx
function App(){
	const someFunc = useCallback( () => {
	function someFunc(){}}, [])

	<Archive someFunc={someFunc} />
}
```

1. If the function is not dependent on any reactive values within the component. *Move em out of the component*.
	- avoids unnecessary re-creation of the function at every re-render.
2. If the function is not called within the component but needed in useEffect dependency. *Move em inside the useEffect*
3. If the function cannot 
	- be moved out cause it uses reactive values from within the component
	- be moved in useEffect because it is called within the component but need in useEffect's dependency array
==Memoize it.==
***
# Lazy Loading
The whole react app is bundled in one JS file which is then shipped off to the client device. This affects the performance if the file is really huge, so in comes the Lazy Part!

1. Import your components using LazyLoading
```jsx
import { lazy } from 'react';

const HomePage = lazy(() => import('./components/HomePage'));
```

2. Wrap the routes with Suspense
```jsx
import { Suspense } from 'react';

<Suspense fallback={<SpinnerFullPage />}>
	<Routes>
		<Route path="/" element={<HomePage />} />
	</Routes>
</Suspense>
```

***
# Redux - Advanced UI state management
Its very similar to the [[#**4. useReducer()**]] hook but its really a scalable approach
## The Classical approach (deprecated)

1. `accountReducer.js` 
```js
//initial states
const initialState = {
	balance = 0
}

//reducers
function accountReducer(state = inititalState, action){
	switch(action.type){
		case 'account/deposit':
			return {
				...state,
				balance: state.balance + action.payload
			}
		case 'account/withdraw':
			return {
				...state,
				balance: state.balance - action.payload
			}
		default:
			return state;
	}
}

//action creators
function deposit(amount){
	return {
		type: 'account/deposit', 
		payload: amount
	}
}
function withdraw(amount){
	return {
		type: 'account/withdraw',
		payload: amount
	}
}

//exports
export { accountReducer, deposit, withdraw }
```

2. `bankReducer.js`
```jsx
//initalstates
const initialState = {
	isAccountOpen: false
}

//reducers
function bankReducer(state = inititalState, action){
	switch(action.types){
		case 'bank/openAccount':
			return {
				...state,
				isAccountOpen: true
			}
		case 'bank/closeAccount':
			return {
				...state,
				isAccountOpen: false
			}
		default:
			return state;
	}
}

//action creators
function openAccount(){
	return { type: 'bank/openAccount' }
}
function closeAccount(){
	return { type: 'bank/closeAccount' }
}

//exports
export { openAccount, closeAccount }
```

3. `store.js`
```js
import { createStore, combineReducers } from 'redux';
import { accountReducer } from './accountReducer';
import { bankReducer } from './bankReducer';

const rootReducer = combineReducer({
	account: accountReducer,
	bank: bankReducer,
})

const store = createStore(rootReducer);
export default store;
```

4. usage within `App.jsx`
```js
import { useSelector, useDispatch } from 'react-redux'
import { deposit, withdraw } from './accountReducer'
import { openAccount, closeAccount } from './bankReducer'

const balance = useSelector( state => state.account.balance )
const isAccountOpen = useSelector( state => state.bank.isAccountOpen )

const dispatch = useDispatch();

dispatch(openAccount())
dispatch(deposit(1000))
dispatch(deposit(500))
dispatch(closeAccount())
```
## The Toolkit's way

1. `accountSlice.js`
```jsx
import { createSlice } from "@reduxjs/toolkit";

const initialState = {
	balance: 0,
}

const accountSlice = createSlice({
	name: 'account',
	initialState,
	reducer: {
		deposit(state, action){
			state.balance += action.payload
		},
		withdraw(state, action){
			state.balance -= action.payload
		}
	}
})

export const { deposit, withdraw } = accountSlice.actions;
export default accountSlice.reducer;
```

2. `bankSlice.js`
```jsx
import { createSlice } from "@reduxjs/toolkit"

const inititalState = {
	isAccountOpen: false,
}
const bankSlice = createSlice({
	name: 'bank',
	inititalState,
	reducer: {
		openAccount(state, action){
			state.isAccountOpen = true
		},
		closeAccount(state, action){
			state.isAccountOpen = false
		}
	}
})

export const { openAccount, closeAccount } = bankSlice.actions;
export default bankSlice.reducer;
```

- the `action` functions can only take one `payload` argument, if we need more than one then we need to use `prepare()`
```jsx
const someSlice = createSlice({
	name: "theSlice",
	initialState,
	reducer: {
		actionOne: {
			prepare(argOne, argTwo){
				return { payload: { argOne, argTwo } }
			},
			reducer: {
				someAction(state, action){
					action.payload.argOne;
					action.payload.argTwo;
				}
			}
		}
	}
})
```
- or we can just pass `{ argOne, argTwo }` as payload argument at use. This counts as one argument instead of `( argOne, argTwo )`
3. 
```jsx
import { configureStore } from "@reduxjs/toolkit";

import { accountReducer } from './accountSlice ';
import { bankReducer } from './bankReducer';

configureStore({
	reducer: {
		account: accountReducer,
		bank: bankReducer 
	},
});

export default store;
```
