---
tags:
---
# React
React is a JavaScript Library aiming for a more reactive web application development. React is based on the idea of [[Imperative VS Declarative Programming |declarative programming]], and uses a special extension to JavaScript (extension `.jsx`). To use React, we need 3 things:
- React: the actual library itself
- ReactDOM: takes React's components and inserts them into the DOM
- Babel: for translating `jsx` into `js` files that browsers actually understand.

React's strength comes from the fact that we can write HTML like scripts directly in our JavaScript Code:
```html
<div id="app"></div>
<script>
	function App() {
		return(
			<div>hello!</div>
		);
	}
	
	ReactDOM.render(<App />, document.querySelector('#app'))
</script>
```
We can even declare variables and pass them into our HTML! To do this, put them inside curly braces like so:
```html
<div id="app"></div>
<script>
	function App() {
		const x = 1;
		const y = 2;
		return(
			<div>hello {x + y}!</div>
		);
	}
	
	ReactDOM.render(<App />, document.querySelector('#app'))
</script>
```

## Components
React divides applications into components. As mentioned before, React is based on declarative programming, so these components most likely will come in the form of a function. These functions can return HTML snippets, and can be called using the `<FunctionName />` syntax, as can be seen above in the `ReacDOM.renter(<App />`) line.

We can even pass parameters, just like functions:
```html
<div id="app"></div>
<script>
	function Hello(props) {
		return (
			<div>Hello, {props.name}!</div>
		);
	}
	function App() {
		return (
			<div>
				<Hello name="Harry" />
				<Hello name="Ron" />
				<Hello name="Hermione" />
			</div>
		)
	}
</script>
```
In react, these "parameters" are referred to as properties, or "props". By using different props, we can get different interactions with the same component.


---
Categories: [[030-Web Development]], [[CS50 - Web Dev]]
References:
