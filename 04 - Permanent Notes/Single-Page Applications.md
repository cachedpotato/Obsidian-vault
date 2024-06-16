---
tags:
---
# Single-Page Applications
Single-Page Applications are applications where everything is done in one page, instead of separate parts being assigned to a different page.

Say we have 3 different parts that we want to show. How can we do it in a single page? one way is to have some sort of toggle, that once toggled, shows only the selected part. Every single page by default will be invisible.

```html
<head>
	<style>
		div {
			display: none;
		}
	</style>
	<script src="SPA.js"></script>
</head>
<body>
	<button data-page="page1">Page1</button>
	<button data-page="page2">Page2</button>
	<button data-page="page3">Page3</button>
	<div id="page1">This is Page 1</div>
	<div id="page2">This is Page 2</div>
	<div id="page3">This is Page 3</div>
</body>

```
inside `SPA.js`:
```js
function showPage(page) {
	document.querySelectorAll('div').forEach(div => {
		div.style.display = 'none';
	});
	document.querySelector(`#${page}`).style.display = 'block';
}

document.addEventListener('DOMContentLoaded', () => {
	document.querySelectorAll('button').forEach(button => {
		button.onclicked = () => {
			showPage(this.dataset.page);
		}
	})
})
```

This way, we will be able to see only one page at a time.

## Single-Page Applications and `fetch`
Cool thing about SPA is that we can incorporate `fetch` as a means of getting the parts that we need from our own server. This way, we don't need to load everything at the same time, and loading can be done asynchronously!
```js
function showSection(section) {
	fetch(`/path/to/${section}`)
	.then(responce => response.text())
	.then(text => {
		console.log(text)
		document.querySelector('#content').innerHTML = text;
	})
	.catch(error => console.log('ERROR: ', error));
}

document.addEventListener('DOMContentLoaded', () => {
	document.querySelectorAll('button').forEach(button => {
		button.onclick = () => {
			showSection(this.dataset.page);
		}
	})
});
```
Now our page is _dynamically loaded_, depending on our needs.

## `history`
Having a single page do everything can be efficient, but it has one problem - URLs. Because the URL stays the same, if we try to load a previous section, we cannot because well, the URL is the same no matter what section we're in!

..That is, unless we have `history`.

`history` takes care of this exact issue. just like `localState` it will store our history of viewed sections, and put it into a stack, which will appear as a part of the URL. this enables us to traverse through previously viewed sections.

```js
window.onpopstate = function(event) {
	console.log(event.state.section);
	showSection(event.state.section);
}

document.addEventListener('DOMContentLoaded', () => {
	document.querySelectorAll('button').forEach(button => {
		button.onclick = () => {
			//add to history
			const section = this.dataset.section;
			history.pushState({section: section}, "", `section${section}`);
			
			showSection(section);
		}
	})
});
```
the `history.pushState()` method takes in three arguments. the first takes in the key-value pair to push, and the third is for how to display it in the URL.

the `window.onpopstate` event is for when we go back in history. As we pop it out of the stack, we call a function, in this case, that logs it in the console and shows the previous section.


---
Categories: [[030-Web Development]], [[CS50 - Web Dev]], [[Asynchronous JavaScript]]
References:
