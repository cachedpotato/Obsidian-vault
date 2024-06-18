---
tags:
---
# Sorting in JavaScript
the `sort()` function in JavaScript can be used by just calling, or we can pass our own custom function that takes two arguments for comparing.

The default is in ascending order.
```js
const fruits = [
	{name: "Apple", calories: 100,},
	{name: "Banana", calories: 80,},
	{name: "Mango", calories: 140,}];

fruits.sort((a, b) => a.name.localeCompare(b.name)); //ALPHABETICAL
fruits.sort((a, b) => b.name.localeCompare(a.name)); //ALPHABETICAL REVERSE
fruits.sort((a, b) => a.calories - b.calories)
```

Basically, we call an anonymous function that returns some "orderable" value, and based on the size of that value we sort them in increasing order. For example, for numeric ordering, we simply get the subtraction of the two elements, and order by value.

---
Categories: [[JavaScript]]
References:
