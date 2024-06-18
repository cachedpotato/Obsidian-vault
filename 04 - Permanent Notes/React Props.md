---
tags:
---
# React Props
props, or properties, are read-only components that can be shared between components. We've already seen examples [[React|before]], so here we'll only be talking about more specific stuff.

## `PropType`
Since JavaScript is a dynamically typed language, it can be hard for other developers looking at my code to figure out exactly what type a certain prop needs to be. For this reason, it's good to add something called `propType` to our props:

```jsx
import propTypes from 'prop-types'

function Student(props) {
	return(
		<div className="student">
			<p>Student Name: {props.name}</p>
			<p>Student age: {props.age}</p>
		</div>
	);
}

Student.propTypes = {
	name: propTypes.string,
	age: propTypes.number,
}

export default Student
```
At the bottom, we defined the types for our props using `Student.propTypes = {...}`. Note that this is purely for debugging purposes, and will only give out warnings if we enter a different type for the corresponding props.

## `defaultProp`
Besides typing, we can also set our default values for our props using `defaultProp`:
```jsx
Student.defaultProp = {
	name: "guest",
	age: 0,
}
```
in `App.jsx`
```jsx
function App() {
	return(
		<>
			<Student name="Spongebob" age="24" />
			<Student name="Patrick" age="30" />
			<Student name="Larry" />
		</>
	);
} 
```
Because we did not set the `age` value for `Larry`, the default value `0` will be used.


---
Categories: [[React]]
References:
