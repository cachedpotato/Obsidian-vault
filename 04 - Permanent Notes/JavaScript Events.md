---
tags:
---
# JavaScript Events
JavaScript is mainly used to make websites interactive, and as said in the [[JavaScript Basics]] section, we implement what's called an 'event-driven programming' to do so. What exactly are events? Hovering? Clicking? The short answer - all of them!

Here are some notable events JavaScript innately supports:
- `onclick`
- `onmouseover`
- `onkeydown`
- `onkeyup`
- `onload`
- `onblur`
Most events start with `on`. Damn looks like a game engine now.

The following is an example of taking input that the user submitted and creating a list below
```js
document.addEventListener('DOMContentLoaded', () => {
	//disable submit on default
	document.querySelector('#submit').disabled = true;

	//enable it only when something is typed and is longer than 0
	document.querySelector('#task').onkeyup = () => {
		if document.querySelector('#task').value.length > 0 {
			document.querySelector('#submit').disabled = false;
		}
	}
	document.querySelector('form').onsubmit = () => {
		const task = document.querySelector('#task').value;
		const li = document.createElement('li');
		
		li.innerHTML = task;
		document.querySelector('#tasks').append(li);
		document.querySelector('#task').value = '';
		return false;
	}
})
```
We not only update our list of tasks (unordered lists) based on user submit (`onsubmit`) events, we also enable and disable the submit button based on if the user pressed a key (`onkeyup`) or not, and if the submission is blank or not.

---
Categories: [[JavaScript]], [[CS50 - Web Dev]], [[030-Web Development]]
References:
