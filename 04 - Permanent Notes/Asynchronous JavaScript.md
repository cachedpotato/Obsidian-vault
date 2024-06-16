---
tags:
---
# Asynchronous JavaScript
As we use APIs of different servers, we have to wait until we get a response, and we do not know (or not "in sync" with) exactly when the data will arrive. We refer to this as being "asynchronous", and JS that deals with asynchronous data is called Asynchronous JavaScript (AJS).

## `fetch` and `promise`
To get a data from API, we use the fetch command like so:
```js
fetch("urltoapi.com");
```
this returns not JSON, but a `promise`. A `promise` means that the data _WILL_ come, but we're just not sure when. once we actually DO get the data, we can do various things with it. In JS, we can do this with `then`.
```js
fetch("urltoapi.com")
.then(response => response.json())
.then(data => {
	console.log(data)
});
```
here, once we first convert it into JSON, and then print it out to our console.

## `catch`
Of course, a `promise`, like in real life, promises can be broken. For error handling, we can add `catch` at the end, like so:
```js
fetch('urltoapi.com')
.then(response => response.json())
.then(data => {
	document.querySelector('h1').innerHTML = data.array['columnname'];
})
.catch(error => console.log('ERROR: ', error));
```

---
Categories: [[API]], [[030-Web Development]], [[CS50 - Web Dev]]
References:
