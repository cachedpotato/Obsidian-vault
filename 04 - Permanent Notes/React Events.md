---
tags:
---
# React Events
Just like how in plain JavaScript we can handle events such as `onclick`, react can do the same, AND can put the handler within the HTML returns!

```jsx
function Button() {
	const handleClick = () => console.log("ouch!")
	return(
		<button onClick = {handleClick}>Click Me!</button>
	);
}
```
React's event names are the same as JavaScript, except for the fact that they're writtn in `camelCase`. the above code is the same as:
```html
<button>Click Me!</button>
<script>
	document.querySelector('button').onclick = () => {
		console.log("ouch!");
	}
</script>
```

## Event Examples
- `onClick` 
- `onDoubleClick`
- `onChange`

## Passing functions with arguments
because we're basically passing functions, we can pass arguments as well:
```jsx
function Button() {
	const handleClick(name) = () => console.log(`${name} stop clicking me`);
	return(
		<button onClick={handleClick("Bro")}>Click Me</button>
	);
}
```
Actually, this does not work as intended. in the console we can see that the `handleClick()` returns immediately as we load our page, without us clicking the button. This is because when we pass strings like this directly, it will instantly return. What we need to do is wrap it within an anonymous function:
```jsx
//--snip
return(
	<button onClick={() => handleClick("bro")}>Click Me</button>
);
```

## Event Handler
Event handler actually has an argument automatically passed. It refers to the event itself, and it's annotated either `event` or `e` in short.
```jsx
function Button() {
	const handleClick = (e) => e.target.textCotent = "OUCH!";
	return(<button onClick={(e) => handleClick(e)}</button>);
}
```
We can access the target of the event through the property `e.target`.
after we get the target, we can use standard JavaScript stuff to change values, styles, etc.
```jsx
function YetAnotherButton() {
	const handleClick = (e) => e.target.style.display = "none";
	return <button onClick={(e) => handleClick(e)}>Click Me</button>
}
```

## `onChange` Event
The `onChange` event is used primarily for, but not limited to, these four elements:
- `input`
- `textarea`
- `radio`
- `select`
this event triggers every time the input changes.
```jsx
use React, {useState} from 'react'
function OnChange() {
	const [name, setName] = useState("Guest")
	function handleNameChnge(event) {
		setName(event.target.value)
	}
	return(
		<input value={name}
			onChange={handleNameChange}
			placeholder="Name Here"
			autoFocus
		/>
	);
}
```

---
Categories: [[React]]
References: