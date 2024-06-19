---
tags:
---
# React Hooks
React Hook is a special function that allows functional components to use React features without using class components. If you see methods that start with `use` such as `useState, useEffect, useContext`, chances are that those are React Hooks.

to use React Hooks, we first need to import them from our library:
```jsx
import React, {useState} from 'react'
```
## State
A State is any kind of data we want to store in our component. to create a state, we use `React.useState(default)`:
```jsx
function App() {
	const [count, setCount] = React.useState(0);

	function updateCount() {
		setCount(count + 1);
	}
	
	return(
		<div>
			<div>{count}</div>
			<button onClick={updateCount}>Count<button>
		</div>
	)
}
```
Here we created a component that returns a `div` that contains a counter and a button that increases the count. we can see that the state `count` is defined as `cosnt [count, setCount] = ...`. While we cannot directly alter our `count` value because of our `const` constraint, we still can with `setCount`, which acts as a method for mutating state values. We use this function in the `updateCount` function, which is defined in our component function `App()`.

As mentioned, state can be _any_ type of data, meaning we can create a struct-like state like so:
```jsx
function App() {
	const [structState, setStructState] = React.useState({
		num1: 0,
		num2: 1,
		answer: ""
		incorrect: false,
	})

	function updateState() {
		setStructState({
			...structState,
			num1: structState.num1 + 1,
			num2: structState.num2 * 3,
		});
	}
}
```
Two things of note:
- to use the fields inside state, we must prefix it with state name (ex: `structState.num1`)
- we can use the `...` syntax to copy over whatever the previous values were when updating

## `useState()`
`useState()` is a React Hook that lets us create a stateful variable and a setter function to change that state, as can be seen above.

## `useEffect()`
This hook tells React to do some code when either one of these happens:
- The component re-renders
- The component mounts (gets appended to the DOM)
- The state of a value changes
This hook takes
- A side function to compute. Any of these is possible as a side function
	- callback
	- anonymous function
	- arrow function
- dependencies (optional)
```jsx
useEffect(() => {})                 //runs after every re-render
useEffect(() => {}, [])             //runs only on mount
useEffect(() => {}, [dependencies]) //runs on mount + value change
```
By adding dependencies, we will activate the function _IFF_ the dependency changes.

Use Effect can be used in a lot of situations, such as:
- Event Listeners
- DOM manipulation
- Real-time updates
- Fetching Data from API
- component cleanup after un-mounting

Be sure to use `useEffect` near the top of the component
```jsx
function MyComponent() {
	const [count, setCount] = useState(0);
	useEffect(() => {
		document.title = `Count: ${count}`
	}, [count]);

	return();
}
```
If we do not have any dependency set but still add the empty array, this will trigger just once, when it first renders. If we do not have the array at all, this will trigger _every time the component gets updated_, no matter the cause.

If we have multiple dependencies, `useEffect()` will trigger when _EITHER_ of them changes.

the empty dependency array is used for first-time mount-only effects. This can be useful for event listeners. instead of creating a listener every time the event is detected, we can do like so:
```jsx 
useEffect(() => {
	window.addEventListener("resize", callbackFunction);

	return(window.removeEventListener("resize", callbackFunction));
})
```
the `return()` is for cleanup. if you have an `eventListener` inside the `useEffect` hook, returning `removeEventListener()` will get rid of the component.

## `useContext()`
`useContext()` hook allows us to share values between multiple _levels_ of components without passing props through each level.
If we were to have 4 Components nested into each other, without using the hook, we would've had to do this:
```jsx
import ComponenB from "./ComponentB"
function ComponentA() {
	const [user, setUser] = useState("");
	return(<><ComponentB user={user}/></>);
}
```
In `ComponentB`
```jsx
import ComponenC from "./ComponentC"
function ComponentB(props) {
	const [user, setUser] = useState("");
	return(<><ComponentC user={props.user}/></>);
}
```
In `ComponentC`
```jsx
import ComponenD from "./ComponentD"
function ComponentC(props) {
	const [user, setUser] = useState("");
	return(<><ComponentD user={props.user}/></>);
}
```
In `ComponentD`
```jsx
function ComponentD(props){
	return(<div><p>{`Bye ${props.user}`}</p></div>)
}
```
This is known as _props drilling_ and can get really tedious really fast. Not to mention you still need to pass it through all levels even if they themselves are not using it. By using the `useContext()` hook, we can simply this process.

To use the `useContext` hook, we just need three steps:
1) `import React, {createContext} from 'react'` from the _PROVIDER_
2) the _PROVIDER_ will create a context by:
```jsx
export const StateContext = createContext();
function MyComponent() {
	const [state, setState] = useState();
	return (
		<div>
			<StateContext.Provider value={state}>
				<ComponentB />
			</StateContext.Provider>
		</div>
	)
}
```
3) the _CONSUMER_ will use the context by:
```jsx
import {StateContext} from "./MyComponent"
import React, {useContext} from 'react'
function ComponentD() {
	const state = useContext(StateContext);
	return(<p>{state}</p>)
}
```
We can have multiple consumers, too!

## `useRef()` Hook
`useRef` hook is used when you want to don't want to cause re-renders on value change but still want to remember that change nonetheless. This is used for:
- Accessing/Interacting with DOM elements
- Handling Focus, Animations and transitions
- Managing timers and intervals

`useRef` returns an object that returns one property `current`. This property can be anything - array, object, even an HTML element!
```jsx
import React, {useRef, useEffect} from 'react'

function MyComponentLoadsOnlyOnce() {
	const inputRef = useRef(null);

	useEffect(() => {
		console.log("COMPONENT RENDERED");
	});

	handleClick() {
		inputRef.current.style.backgroundColor = "yellow";
		inputRef.current.focus();
	}

	return(
		<div>
			<button onClick={handleClick}>Click Me</button>
			<input ref={inputRef} />
		</div>
	)
}
```
the `ref` attribute in the `<input>` element is a special attribute that creates reference to a value. Here, we passed `inputRef`. This code will make the input field change background color to yellow when clicked. This is because the `input` tag holds a reference `inputRef`, and when `handleClick` is called we change the values of `inputRef`'s `current` .
![[Pasted image 20240618155948.png|600]]
As mentioned, `useRef` object does not re-render components. if we check the console log, we would only see `COMPONENT RENEDERED` once, whereas if we used `useState()`, we would've seen the message every time the input field has been changed.



---
Categories: [[React]], [[030-Web Development]]
References:
