---
tags:
---
# JavaScript Local Storage
Say we have a page that tracks the number of times users have clicked a button:
```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<title>Counter</title>
		<script src="counter.js"></script>
	<head>
	<body>
		<h1>Count: 0</h1>
		<button id="button">Click Me!</button>
	</body>
</html>
```

```js
let counter = 0;
document.addEventListener('DOMContentLoaded', () => {
	document.querySelector('#button').onclicked = () => {
		counter++;
		document.querySelector('h1').innerHTML = `Count: ${counter}`;
	}
});
```
This page will work, but whenever we refresh the page, the counter will go back to 0. Sometimes this is desirable, but there are some data we want to store on a per-user basis. JavaScript lets us do just that, by utilizing what's called a `localStorage`.

## `LocalStorage` item
`localStorage` can be thought of as a [[Hash Map]], because it's stored in key: value pairs. for the example above, `counter` will be the key and the integer value will be the value. To retrieve or create value, we do the following:
```js
if (!localStorage.getItem('counter')) {
	localStorage.setItem('counter', 0)
}

document.addEventListener('DOMContentLoaded', () => {
	document.querySelector('#button').onclick = () => {
		let counter = localStorage.getItem('counter');
		counter++;
		document.querySelector('h1').innerHTML = `Count: ${counter}`;
		localStorage.setItem('counter', counter);
	}
});


```

---
Categories: [[JavaScript]], [[CS50 - Web Dev]]
References:
