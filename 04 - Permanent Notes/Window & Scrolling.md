---
tags:
---
# Window
A window is the _visible_ part of the _document_, which is the entirety of our webpage. Think of a REALLY long Wikipedia page for example. We cannot fit all that text into our monitor at once, unless we zoom the hell out. Normally, we would have only a portion of the entire page visible, like the diagram below:
![[Pasted image 20240615173758.png|500]]

## Window Properties
- `window.scrollX`: Shows number of pixels scrolled right
- `window.scrollY`: Shows number of pixels scrolled down
- `document.body.offsetHeight`: The height of the entire document
- `window.innerHeight`: Size of the height of the window
- `window.innerWidth`: Size of the width of the window
Using these properties, we can add more interactivity based on user scroll.

```js
window.onscroll = () => {
	if (window.scrollY + window.innerHeight >= document.body.offsetHeight) {
		document.querySelector('p').style.color = "green";
	} else {
		document.querySelector('p').style.color = "white";
	}
}
```

## Scrolling & Page Loading
The above example is rather impractical, so let's look at a more practical use case. what if we want to dynamically add new content as the user reaches the end of the document (a la Reddit)?

What we need are:
- an [[API]] that stores chunks of data that will be appended asyncronously
- a `load` function that will load posts
- an `add_content` function that will add to the page new contents given a specific range
- an `eventListener` that will automatically call the `load` function at first
- a `onscroll` event trigger that will continuously call `load` once we reach the bottom of the screen
```js
let counter = 0;
let quantity = 20; //chunks of posts

//initial load
document.addEventListener('DOMContentLoaded', load);

//get contents from API and load
function load() {
	const start = counter;
	const end = counter + quantity - 1;
	counter = end + 1;

	//fetch from API posts that we need to load
	fetch(`/posts?start=${start}&end=${end}`)
	.then(response => response.json())
	.then(data => {
		data.posts.forEach(add_content);
	})

//from content crate div
function add_content(contents) {
	//create div
	const post = document.createElement('div')
	post.innerHTML = contents;

	//post to master
	document.querySelector('#posts').append(post);
}

//dynamic loading by scroll event detection
window.onscroll = () => {
	if (window.scrollY + window.innerHeight >= document.body.offsetHeight)  {
		load();
	}
}
```
The Payload:
```json
{
	"posts": {"post#20", "post#21", "post#22",//...}
}
```
from our own `posts` API, we get JSON payloads that looks like this. We can see that in the JS code we access the contents of JSON using `data.posts`, which in turn returns an array, and we apply a `forEach` operation to add content.

---
Categories: [[030-Web Development]], [[CS50 - Web Dev]], [[JavaScript]]
References:
