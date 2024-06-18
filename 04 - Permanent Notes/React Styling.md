---
tags:
---
# React Styling
React's styling can be done in three ways: External, Module and Inline. Let's take a brief look at each of them

## 1. External Styling
This is the "Standard" way of styling that we are all accustomed to. in a separate CSS file, create styling for the component:
```jsx
function Button() {
	return(
		<button className="button">Click Me</button>
	);
}
```
In our main `App.jsx`:
```jsx
import Button from "./Button"
Function App() {
	return(
		<Button />
	);
}
```
In index.css:
```css
.button {
	border-radius: 20px;
	padding: 10px 20px;
	background-color = #FF1231;
}
```
While this is a completely valid way of doing things and are used for global styles and small projects, as our app grows bigger it can get increasingly harder to keep track of all the class names, especially with bad naming conventions like the example above. Instead, we can be a bit "modular" with our approach.

## 2. Modular
within our assets directory, we can create a separate directory for our component. We can then define and style our component there. The strength in this approach is that things are now a lot more modular:

in our `assets/Button/Button.jsx`
```jsx
import styles from "Button.module.css"
Function Button() {
	return(
		<button className={styles.button}>Click Me</button>
	);
}
```
in our `App.jsx`
```jsx
import Button from "/Button/Button.jsx"
//--snip
```
While most text editors will take care of import paths when we move things around, it's always best to double check if things are set correctly.
While being modular is cool and all, this can be too much of a hassle if we're just doing minor/small styling for a small component. In situations like that, we can use inline styling.

## 3. In-line
```jsx
function Button() {
	const styles = {
		borderRadius: "20px",
		padding: "10px 20px",
		backgroundColor: "#FF1231",
	}
	return(
		<button style={styles}>Click Me</button>
	);
}
```
If we don't want to create a variable, we can just put the entire styling within _TWO CURLY BRACES_:
```jsx
function Button() {
	return(
		<button>
			style = {{
				borderRadius: "20px",
				padding: "10px 20px",
				backgroundColor: "#FF1231",
			}}
		</button>
	);
}
```
here we define a constant `styles` that has the identical style guide as the CSS example above. There are some changes though:
- we need to use camelCase
- the values are strings
- we use commas instead of semicolons
- instead of `className` we use `style={styles}`

For complex styling, obviously in-line approach is bad, so try to use this for super simple styling only.



---
Categories: [[React]]
References:
