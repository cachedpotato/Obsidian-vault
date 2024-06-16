---
tags:
---
# JavaScript Methods
## `querySelector()` and `innerHTML`
`querySelector()` grabs a certain portion of the HTML file (passed as an argument) and returns that.
```JS
document.querySelector('h1')
```
this will grab the `<h1>` tag in the HTML file. to access to what's _INSIDE_ this tag, We need to extract that using `innerHTML`:
```JS
function helloGoodbye() {
	document.querySelector('h1').innerHTML = 'Goodbye!';
}
```

There is also `querySelectorAll()` function that gets all the queries that matches the argument and returns an array:
```js
function stuff() {
	let arr = document.querySelectorAll('button');
	alert(`yo ${arr[0]}`);
}
```
we can also iterate over the elements using the `forEach()` method.
```javascript
document.addEventListener('DOMContentLoaded', function() {
	document.querySelectorAll('button').forEach(function(button) {
		button.onclick = function() {
			document.querySelector('h1').innerHTML = button.dataset.color
		}
	});
});
```

## `addEventListener`
This method creates a listener (often times a function) for a certain event. When the event is triggered, the Listener will do whatever action is provided.
```JS
function stuff() {
	document.addEventListener('DOMContentLoaded', function() {
		document.querySelector('button').onclick = function() {
			document.querySelector('h1').innerHTML = 'stuff';
		}
	});
}
```


---
Categories: [[JavaScript]], [[CS50 - Web Dev]]
References:
