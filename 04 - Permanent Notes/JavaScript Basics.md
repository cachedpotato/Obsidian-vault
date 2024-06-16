---
tags:
---
# JavaScript Basics
JS lets us change the contents of our website based on user interaction, often called events. Creating code to change websites based on such events is called _event-driven programming_, and JS lets us do just that. Let's look at how JS can manipulate HTML.

## Triple equal sign and double equal sign
`/===`  sign is for strict checking, where the value _AND THE TYPE_ must be the same and `/==` is for weaker form of checking, where only the value needs to be the same.
```JS
function toggleableHello() {
	let heading = document.querySelector('h1');
	if (heading.innerHTML === 'Hello') {
		heading.innerHTML = 'Goodbye';
	} else {
		heading.innerHTML = 'Hello'
	}
}
```

## String Formatting
JS uses the `${}` syntax, similar to bash script, for string formatting.
```JS
let count = 0;
function counter() {
	count += 1;
	if (count % 10 === 0) {
		alert(`count is now ${count}`);
	}
}
```

## `this`
`this` acts like `self` in Python or Rust, and refers to itself.
```js
document.querySelector('select').onchange = function() {
	document.querySelector('#id').style.color = this.value;
}
```
Use the `this` keyword when we're inside an event handler, as is the case above (`onchange`)


---
Categories: [[JavaScript]], [[CS50 - Web Dev]]
References:
