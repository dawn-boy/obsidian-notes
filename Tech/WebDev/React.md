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

1. Create a separate `MyContext.jsx` file
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
# Global UI states vs remote states
## Global UI states
These are the states that reside locally in the application, controlling the UI behavior across components.
## Global remote states
These are the data fetched or transferred to the server (using an API). They usually reside in the servers.
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
	balance: 0
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

const rootReducer = combineReducers({
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
	reducers: {
		deposit(state, action){
			state.balance += action.payload
		},
		withdraw(state, action){
			state.balance -= action.payload
		}
	}
})

export const { deposit, withdraw } = accountSlice.actions;
export default accountSlice.reducers;
```

2. `bankSlice.js`
```jsx
import { createSlice } from "@reduxjs/toolkit"

const initialState = {
	isAccountOpen: false,
}
const bankSlice = createSlice({
	name: 'bank',
	inititalState,
	reducers: {
		openAccount(state, action){
			state.isAccountOpen = true
		},
		closeAccount(state, action){
			state.isAccountOpen = false
		}
	}
})

export const { openAccount, closeAccount } = bankSlice.actions;
export default bankSlice.reducers;
```

- the `action` functions can only take one `payload` argument, if we need more than one then we need to use `prepare()`
```jsx
const someSlice = createSlice({
	name: "theSlice",
	initialState,
	reducers: {
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

const store = configureStore({
	reducers: {
		account: accountReducer,
		bank: bankReducer 
	},
});

export default store;
```
## CreateAsyncThunks
```js
import { createSlice, createAsyncThunk } from '@reduxjs/toolkit'  
import { getData } from '../services/apiRequests.js'  
  
export const fetchData = createAsyncThunk('api/fetchdata', async () => {  
  const data = await getData()  
  return data  
})  
  
const initialState = {  
  payload: '',  
  status: 'idle', // idle, loading, succeeded, failed  
  action: '',  
  error: '',  
}  
  
const apiSlice = createSlice({  
  name: 'api',  
  initialState,  
  reducers: {},  
  extraReducers: builder => {  
    builder  
      .addCase(fetchData.pending, state => {  // always use {}, wont work without it
        state.status = 'loading'  
      })  
      .addCase(fetchData.fulfilled, (state, action) => {  
        state.status = 'succeeded'  
        state.payload = action.payload.payload  
        state.action = action.payload.action  
      })  
      .addCase(fetchData.rejected, (state, action) => {  
        state.status = 'failed'  
        state.error = 'Failed to fetch the API data'  
      })  
  },  
})  
  
export default apiSlice.reducer
```
***
# Temporary API mountpoint

1. Install `json-server`
```sh
npm install json-server --save-dev
```

2. add to `package.json`
```json
scripts: {
	...
	"server": "json-server --watch ./data/questions.json --port 6000"
}
```

3. run server
```bash
npm run server
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

## React Router
# A sample project structure
```
-- Project
|
|- /src
|  |-- /features   // for main pages of the site
|  |  |-- /cart
|  |  |-- /order
|  |  |-- /menu
|  |  |-- /user
|  |  |
|  |-- /services   // for api management
|  |-- /ui         // for misc ui elements, like navbar, etc
|  |-- /utils      // for helper functions
```

### A New way of declaring routes!
Inside `App.jsx`
```jsx
import { RouterProvider, createRouterProvider } from "react-router-dom";

const router = createRouterProvider([
	{
		element: <AppLayout />,
		children: [
			{
				path: '/',
				element: <Home />,
				errorElement: <ErrorPage />
			},
			{
				path: '/menu',
				element: <Menu />
			}
		]
	}
])

function App(){
	return <RouterProvider router={router} />
}

//inside <ErrorPage />
import { useRouteError } from 'react-router-dom';
const message = useRouteError().data
```

1. `services/apiQuestions.js`
```js
async function getQuestions(){
	try{
		const response = await fetch(api-url);
		const data = await response.json();
		return data;
	} catch(error){
		console.log(error);
		return -1;
	}
}

export { getQuestions };
```

2. `features/GamePlay.jsx` - inside the component that needs the data.
```jsx
import { useLoaderData } from 'react-router-dom';
import { getQuestions } from '../services/apiQuestions'

function GamePlay(){
	return <div></div>
}

export async function loader(){
	const questions = await getQuestions();
	return questions;
}

export default GamePlay;
```

3. `App.jsx`
```jsx
import { RouterProvider, createRouterProvider } from 'react-router-dom';
import { loader as questionsLoader } from './features/GamePlay'
import GamePlay from './features/GamePlay'

const router = [
	{
		path: '/gameplay',
		element: <GamePlay />,
		loader: questionsLoader
	}
]

function App(){
	return <RouterProvider router={router} />
}
```

***
# Supabase
- an awesome opensource database
1. create a `supabase.js`
```jsx
//npm install @supabase/supabase-js

import { createClient } from '@supabase/supabase-js'
const supabase = createClient(SupabaseURL, SupabaseKey)

export default supabase;
```

2. quering databases
```jsx
//select
const { data, error } = await supabase
	.from('users')
	.select('*');

//insert
const { data, error } = await supabase
	.from('users')
	.insert([{ user: "someone", isOnline: false}])

//update
const { data, error } = await supabase
	.from('users')
	.update({ done: true})
	.eq({'id': 1});

//delete
const { data, error } = await supabase
	.from('todos')
	.delete()
	.eq('id',1)

//uploads
const { data, error } = await supabase
	.storage
	.from('avatars')
	.upload('public/avatar1.png', file)

```
***
# React Query
- Its a data fetching and caching library for react 

1. Initial
```jsx
//npm i react-query react-query-dev-tools
import { QueryClient, QueryClientProvider } from '@tanstack/react-query';
import { ReactQueryDevTools } from '@tanstack/react-query-dev-tools'

const queryClient = new QueryClient({
	defaultOptions: {
		queries: {
			staleTime: 60;
		}
	}
})

<QueryClientProvider client={queryClient} >
	<ReactQueryDevTools initialIsOpen={false} />
	<App />
</QueryClientProvider>
```

2. Fetching data
```jsx
import { useQuery } from '@tanstack/react-query'

const { data, status } = useQuery({
	queryKey: ['users'],
	queryFn: fetchUsers, // must return a promise
});
```
- `queryKey`: unique id for caching
- `queryFn`: async function that returns data

3. Re-fetching
```jsx
const query = useQuery({ ... })
query.refetch()
```

4. Mutation
```jsx

const queryClient = useQueryClient(); // a speacial hook that gives you access to the query client from where ever you are!

const { isLoading: someAlias, mutate } = useMutation({
	mutationFn: (id) => someFunc(id),
	// or mutationFun: someFunc --> if the params are same
	onSuccess: () => {
		toast.success("You're done for")
		queryClient.invalidateQueries({
			queryKey: ['users']
		});
		reset();
		
	onError: error => alert(error)
})
```

***
# React hot toast
- its a notification pop up library. use it as an alternative to `alert()`

1.  Add the `<Toaster />` component to the `<App />`
```jsx
// npm i react-hot-toast

<Toaster position="top-center"
		gutter={12}
		containerStyle={{margin: "8px"}}
		toastOptions={{
			success: {
				duration: 3000
			},
			error: {
				duration: 5000
			},
			style: {
				fontSize: '16px',
				maxWidth: '500px',
				padding: '16px 24px',
				backgroundColor: red;
			}
		}}
/>

toast.success("success")
toast.error("error")
```

***
# React hook forms

1. initialize
```jsx

//npm install react-hook-form
import { useForm } from 'react-hook-form';

const { register, handleSubmit, formState: { errors }} = useForm();

function onSubmit(data){
	console.log(data)
}
function onError(error){
	console.log(error)
}

// the { errors } and the OnError function has the same error data.

<form onSubmit={handleSubmit(onSubmit,onError)}>
	<input id='name' {
		...register('name'), 
		{
			required: "This field is required",
		}
	} />
	<input id='num' {
		...register('num'),
		{
			required: "This field is required",
			// make it optional on a condition
			required: isCondition ? "req" : false
			min: {
				value: 1,
				message: "Should atleast be 1"
			}
			// or a validate function
			validate: (value) => value > 100 || "should be atleas 100"
		}
	}
	//optionally show a text near the input if there's an error
	{errors?.num?.message && <p>{errors.num.message}</p>}
</form>
```
- we're calling the `handleSubmit(onSubmit)` at `onSubmit` property. 
	- It allows the form hook to get all the data from the form,
	- validates them if there's any rules
	- prevents default browser submission
	- and then finally passes the data to your `onSubmit()` function call 

- disable the input and buttons while submitting
```jsx
<input disabled={isCreating} />
<button disabled={isCreating}> Submitting </button
```
- `isCreating` is returned from the `useMutation()` function
### retrieving uploaded files
```jsx
function uploadImg(data){
	const url = "https://something"
	const imageName = `${Math.random()}-${data.image.name}.replaceAll('/','')`
	const imageUrl = `${url}/storage/v1/object/public/bucket-name/${imageName}`

	const { data, error } = await supabase
		.from('bucket-name')
		.insert([{ ...data, image: imageUrl }])
	if(error) throw new Error('youre done for')

	const { error: StorageError } = await supabase
		.from('bucket-name')
		.upload(imageName, data.image)

	if(StorageError){
		await supabase
			.from("bucket-name")
			.delete()
			.eq("id", data.id);
		console.log("Image was not uploaded successfully")
		throw new Error("You're done for.")
	}
```

***
# Advanced React Patterns
## 1. Render props pattern
In this pattern, the component receives a function as a prop (usually called children or render), that it calls to determine what to render.
1. The Usual implementation would be
```jsx
function ObjectList(title, items){
	return(
		<div>
			<h1>{title}</h1>
			{ items.map(obj => <ObjectItem name={obj.name} price={obj.price} /> )}
		</div>
	)
}
function ToyList(title, items){
	return(
		<div>
			<h1>{title}</h1>
			{ items.map(toy => <ToysItem name={toy.name} price={toy.price} /> )} 
		</div>
	)
}

function App(){
	return(
		<div>
			<ObjectList title={"Objects"} items={["one","two","three"]} />
			<ToysList title={"Toys"} items={["one","two","three"]} />
		</div>
	)
}
```

2. But the same implementation in through render props would be
```jsx
function List(title, items, render){
	return(
		<div>
			<h1>{title}</h1>
			<h2>Items</h2>
			{items.map(render)}
		</div>
	)
}

function App(){
	return(
		<div>
			<ObjectList 
				title={"Objects"} 
				items={["one","two","three"]} 
				render={obj => <ObjectItem name={obj.name} price={obj.price} /> }
			/>
			<ToysList
				title={"Toys"} 
				items={["one","two","three"]} 
				render={toy => <ToysList name={toy.name} price={toy.price} /> }
			/>
		</div>
	)
}
```
- much more re-usability!
## 2. Higher Order function Pattern
This pattern takes a component as the input, adds more functionality to it and returns the enhanced component!

1. Definition
```jsx
function withToggles(WrappedComponent){
	return function Toggle(props){
		const [toggle, setToggle] = useState(false)

		return (
			<div>
			{ toggle && <WrappedComponent x{...props} /> }
			<button onClick={ () => setToggle(prev => !prev) } >
				{ toggle ? "Hide" : "Show" }
			</button>
			</div>
		)
	}
}
```

2. Usage
```jsx
const ToggleList = withToggles(List);

<ToggleList title="Something" />
```
- the props given here will be automatically passed to the `WrappedComponent` that's passed.
## 3. Compound Component Pattern

1. Definition
```jsx
import { useContext, createContext, useState } from 'react'

// 1. Create a context
const CounterContext = createContext();

// 2. Create a parent component
function Counter({ children }){
	const [count, setCount] = useState(0);
	const increase = () => setCount(c => c + 1);
	const decrease = () => setCount(c => c - 1);

	return(
		<CounterContext.Provider value={{ count, increase, decrease }}>
			<span>{ children }</span>
		</CounterContext.Provider>
	)
}

// 3. Create a child component
function Count(){
	const { count } = useContext(CounterContext);
	return <span>{ count }</span>
}
function Label({ children }){
	return <span>{ children }</span>	
}
function Increase({ icon }){
	const { increase } = useContext(CounterContext);
	return <button onClick={ increase }>{ icon }</button>
}
function Decrease({ icon }){
	const { decrease } = useContext(CounterContext);
	return <button onClick={ decrease }>{ icon }</button>
}

// 4. Add the children, Since functions are basically objects in js, we can do this.
Counter.Count = Count;
Counter.Label = Label;
Counter.Increase = Increase;
Counter.Decrease = Decrease;

export default Counter;
```

2. Usage
```jsx
// so instead of this
<Counter
iconIncrease="+"
iconDecrease="-"
label="My NOT so flexible counter"
hideLabel={false}
hideIncrease={false}
hideDecrease={false}
positionCount="top"
/>

// we can do this
<Counter>
<Counter.Label>My super flexible counter</Counter.Label>
<Counter.Decrease icon="-" />
<Counter.Increase icon="+" />
<Counter.Count />

</Counter>
```

***
# Environment keys 

1. Create a `.env` file at the root folder
```
VITE_VARNAME=""
```

2. Usage with your app
```jsx
const VARNAME = import.meta.env.VARNAME;
```

***
## Authentication and Authorization
## Register
1. in `apiAuth.js` file
```jsx
async function registerApi({ email, password }) {  
  const { data, error } = await supabase.auth.signUp({ email, password })  
  if (error) throw new Error(`Error signing up: ${error.message}`)  
  return data  
}
```

2. create a `useRegister.js`
```jsx
import { useMutation, useQueryClient } from 'react-query'  
import { registerApi } from '../../services/apiAuth.js'  
import toast from 'react-hot-toast'  
import { useNavigate } from 'react-router-dom'  
  
function useRegister() {  
  const navigate = useNavigate()  
  const queryClient = useQueryClient()  
  
  const { mutate: register, isLoading } = useMutation({  
    mutationFn: registerApi,  
    onSuccess: data => {  
      queryClient.setQueryData(['user'], data.user)  
      toast.success('Registeration successful')  
      navigate('/profile', { replace: true })  
    },  
    onError: () => {  
      toast.error('Registeration failed')  
    },  
  })  
  
  return { register, isLoading }  
}  
  
export { useRegister }
```

3. use in signup
```jsx
import { useRegister } from './useRegister.js'  
  
const SignUp = () => {  
  const { register } = useRegister()  
  
  return (  
    <div>  
      This is the SignUp page.  
      <button  
        onClick={() =>  
          register({ email: 'ad@gmak.com', password: 'adfdfdf34343f@' })  
        }  
      >  
        Register  
      </button>  
    </div>  )  
}  
  
export default SignUp
```
## Login
1. create an `apiAuth.js` file
```jsx
import supabase from './supabase'  
  
async function loginApi(email, password) {  
  let { data, error } = await supabase.auth.signInWithPassword({  
    email,  
    password,  
  })  
  
  if (error) throw new Error(`Error signing in: ${error.message}`)  
  
  return data  
}  
  
export { loginApi }
```

2. create a custom hook `useLogin.js`
```jsx
import { loginApi } from '../../services/apiAuth.js'  
import { useMutation, useQueryClient } from 'react-query'  
import { useNavigate } from 'react-router-dom'  
import toast from 'react-hot-toast'  
  
function useLogin() {  
  const navigate = useNavigate()  
  const queryClient = useQueryClient()  
  
  const { mutate: login, isLoading } = useMutation({  
    mutationFn: ({ email, password }) => loginApi(email, password),  
    onSuccess: user => {  
      queryClient.setQueriesData(['user'], user)  
      toast.success('Login successful')  
      navigate('/profile', { replace: true })  
    },  
    onError: () => {  
      toast.error('Login failed')  
    },  
  })  
  
  return { login, isLoading }  
}  
  
export { useLogin }
```

3. use it in the app
```jsx
import { useState } from 'react'  
import { useLogin } from './useLogin.js'  
  
const Login = () => {  
  const [email, setEmail] = useState('')  
  const [password, setPassword] = useState('')  
  const { login, isLoading } = useLogin()  
  
  function handleSubmit(e) {  
    e.preventDefault()  
  
    if (!email || !password) return alert('Please fill in all fields')  
    login({ email, password })  
  }  
  
  return (  
    <form onSubmit={handleSubmit}>  
      <input        
        type="email"  
        placeholder="Email"  
        onChange={e => setEmail(e.target.value)}  
        disabled={isLoading}  
      />  
      <input        
        type="password"  
        placeholder="Password"  
        onChange={e => setPassword(e.target.value)}  
        disabled={isLoading}  
      />  
      <button disabled={isLoading}>{ isLoading ? "Loading" : "Login" }</button>  
    </form>  )  
}  
  
export default Login
```
## Logout
1. inside `apiAuth.js`
```jsx
async function logoutApi() {  
  const { error } = await supabase.auth.signOut()  
  if (error) throw new Error(`Error signing out: ${error.message}`)  
}
```

2. create a `useLogout.js`
```jsx
import { useMutation, useQueryClient } from 'react-query'  
import { logoutApi } from '../../services/apiAuth.js'  
import toast from 'react-hot-toast'  
import { useNavigate } from 'react-router-dom'  
  
function useLogout() {  
  const navigate = useNavigate()  
  const queryClient = useQueryClient()  
  const { isLoading, mutate: logout } = useMutation({  
    mutationFn: logoutApi,  
    onSuccess: () => {  
      queryClient.removeQueries('user')  
      toast.success('Logout successful')  
      navigate('/', { replace: true })  
    },  
    onError: error => {  
      toast.error(`Logout failed ${error.message}`)  
    },  
  })  
  
  return { isLoading, logout }  
}  
  
export { useLogout }
```

3. usage in app
```jsx
const Profile = () => {  
  const { isLoading, logout } = useLogout()  
  if (isLoading) return <Loading />  
  
  return (  
    <div>  
      This is the Profile page.  
      <button onClick={logout}>Logout</button>  
      <Outlet />    
    </div>)  
}
```

## Authorization - Protecting routes 

### The Basic way
1. inside `apiAuth.js`
```jsx
async function getCurrentUser(){
	// we check if we have the user object in the session
	const { data: session, sessionError } = await supabase.auth.getSession()  
	if (!sessionError) throw new Error(`Error getting a session`)  

	// if so, then we fetch the user from online for up-to-date results
	const { data, userError } = await supabase.auth.getUser()
	if (userError) throw new Error(`Error getting a user`)  

	// we return the info
	return data?.user

}
```

2. create an `useUser` hook
```jsx
import { getCurrentUser } from '../../services/apiAuth.js'  
import { useQuery } from 'react-query'  
  
function useUser() {  
  const { data: user, isLoading } = useQuery({  
    queryKey: ['user'],  
    queryFn: getCurrentUser,  
  })  
  return { isLoading, isAuthenticated: user?.role === 'authenticated' }  
}  
  
export { useUser }
```

3. Create a `<ProtectedRoute />` component to wrap all the routes that needs securing. wrap em.
```jsx
import { useUser } from '../features/login/useUser.js'  
import { Outlet } from 'react-router-dom'  
  
function ProtectedRoute({ children }) {  
  const { isLoading, isAuthenticated } = useUser()  
  
  if (isLoading) return <div>Loading...</div>  
  if (!isAuthenticated && !isLoading)  
    return <div>You must be logged in to view this page.</div>  
  
  console.log(isAuthenticated)  
  if (isAuthenticated) return <Outlet />  
}  
  
export default ProtectedRoute
```
### The Optimized way 
this way uses a provider and the `onAuthStateChange()` function from `supabase`

- do the `<ProtectedRoute />` this way
```jsx
import { useEffect, useState } from 'react'  
import { Outlet } from 'react-router-dom'  
import supabase from '../services/supabase.js'  
  
const ProtectedRoute = () => {  
  const [user, setUser] = useState(null)  
  const [isLoading, setIsLoading] = useState(true)  
  
  useEffect(() => {  
    const { data: user } = supabase.auth.getUser()  
    setUser(user)  
    setIsLoading(false)  
  
    const { data } = supabase.auth.onAuthStateChange((event, session) =>  
      setUser(session?.user ?? null)  
    )  
  
    return () => data.subscription.unsubscribe()  
  }, [])  
  
  if (isLoading) return <div>Loading...</div>  
  if (!isLoading && !user)  
    return <div>You must be logged in to access this page.</div>  
  
  if (user) return <Outlet />  
}  
  
export default ProtectedRoute
```

***
# Error boundaries

```jsx
// npm install react-error-boundary

import { ErrorBoundary } from 'react-error-boundary'
import ErrorPage from './Errorpage.jsx'

<ErrorPage 
	FallbackComponent={ErrorFallback} 
	onReset={() => window.location.replace('/')}
>
	<App />
</ErrorPage>
```