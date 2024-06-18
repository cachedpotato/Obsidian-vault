---
tags:
---
# Modifying Lists in JavaScript
Modifying arrays in JS is pretty...Interesting. Here are some operations (swapping, adding) that are pretty useful.

## Spread Operation
The spread operation `...` grabs whatever the list or an object's fields are not changed within the code and replace them with the previous values. For example,
```js
let myList = [1, 2, 3, 4, 5];
myList = [...myList, 6];
```
This is the same as adding to the array because the spread operation grabs all the elements in the list. This can also be used in objects:
```js
let myObject = {
	field1: "a",
	field2: "b",
	field3: 3,
	field4: 4,
};

myObject = {
	...myObject,
	field4: 5,
};
```

## Swapping entries in array
```js
let myArray = [1, 2, 3, 4, 5, 6];
function swap(index) {
	let swappedArray = [...myArray];
	[swappedArray[index], swappedArray[index - 1]] = 
	[swappedArray[index - 1]], swappedArray[index];
}
```
This removes the need of creating a temporary value for swapping. Here we take an _array_ of two elements of the list we want to swap, and simply swap the two positions.





---
Categories: [[JavaScript]]
References:
