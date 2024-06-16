---
tags:
---
# Arrow notation in JS
Arrow notation `/=>`, also known as a _fat arrow_, is an alternative method for defining anonymous functions. Instead of
```js
document.addEventListener('DOMContentLoaded', function() {
	document.querySelectorAll('h1').forEach(function(button) {
		document.querySelector('#id').style.color = button.style.colors;
	})
})
```
, we can instead do this:
```js
document.addEventListener('DOMContentLoaded', () => {
	document.querySelectorAll('button').forEach(button => {
		document.querySelector('#id').style.color = button.style.colors;
	})
})
```
So `() => {}` is a shorthand for `function() {}`.

Damn JavaScript looking more like a purely functional language by the day.

---
Categories: [[JavaScript]], [[CS50 - Web Dev]]
References:
