---
tags:
---
# JavaScript
Whereas CSS manages the aesthetics of a webpage, JavaScript adds functionality. Just like how CSS is just the code you'd normally write inside the `<style>` tag, JavaScript is something you'd put in the `<script>` tag:

```HTML
<!DOCTYPE html>
<html lang="en">
	<head>
		<script>
			function greet() {
				alert('hello' + document.querySelector('#name').value);
			}
		</script>
	</head>
	<body>
		<form onsubmit="greet(); return false;">
		<input id="name" autofocus autocomplete="off" placeholder="query">
		<input type="submit">
		</form>
	</body>
</html>
```
Also unlike CSS, JavaScript is an ACTUAL CODING LANGUAGE!

## JavaScript and CSS
JS and CSS are very close and intertwined in the context of web development. you can change CSS attributes (and therefore style attributes) with JS, but there's one small catch: Unlike CSS, JS cannot use `kebab-case`, as it can be mistaken for a `-` operator. Instead, JS will use `camelCase` counterpart. 

For example, CSS has an attribute `background-color`, which sets the color of the background. to change this value in JS:
```JavaScript
let body = document.querySelector('body');
document.querySelector('#red').addEventListener('click', function(event){
	body.style.backgroundColor = 'red';
});
```

A bit different than what we've been talking about here, but from the code above, we can see that JS can be used as a functional programming language, where everything is pretty much a call to a function, without any imperative `for` or `while` loops.

---
Categories: [[Web Development]], [[Hypertext Markup Language]],[[CS50 - Introduction]]
References:
Created: 2024-06-14
