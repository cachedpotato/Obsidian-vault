---
tags:
---
# React Updater Functions
An updater function is a function passed as an argument to `setState()` operation. This allows for safe updates based on previous state, and can be used in multiple state updates in asynchronous functions. It's considered good practice to use updater functions whenever we use `setState`.

```jsx
import React, {useState} from 'react'
function MyComponent() {
	const [state, setState] = useState(1);
	function handleChange() {
		setState(s => s + 1);
		setState(s => s + 1);
	}
}
```
Normally, using `setState` continuously like this will NOT result in the state being updated twice. Rather, it will appear as if it's only been handled once. This is because React processes these in batches for performance reasons. With the use of updater functions, however, we can bypass this problem.

Updater Function's naming convention for their argument is one of the two: first letter of the state (`s` for state in this case) or add a prefix `prev` to our state name (`prevState`).

## Updater Functions on Object States
Objects are declared with curly brackets. However, if we're trying to use updater function, just useing the curly brackets will not work. Instead, we need to wrap it inside parentheses:

```jsx
function MyComponent() {
	const [state, setState] = useState({
		id: 0,
		name: "John",
		email: "johny@example.com"
	})

	function handleIDChange(event) {
		setState(s => ({
			id: event.target.value,
		}))
	}

	return(
		<div>
			<input type="text" value="id" onClick={handleIDChange} placeholder="id"/>
		</div>
	)
}
```

---
Categories: [[React]]
References:
