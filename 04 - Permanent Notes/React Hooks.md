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



---
Categories: [[React]], [[030-Web Development]]
References:
