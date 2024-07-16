---
tags:
---
# Pseudo-Class and Pseudo-Element

## Pseudo-class
### `:hover`
This is for hover "events". If we hover over this element, whatever's inside this pseudo-class will render:
```scss
.random_button {
	border: 3px solid #ff2daa;
	border-radius: 50%;
	background-color: #fff;

	&:hover {
		background-color: #123113;
		transition: all 0.3s ease-in;
	}
}
```

## Pseudo-element

### `::before` and `::after`
these pseudo-elements are for adding content _before_ and _after_ the element.
For example, say we have some text:
```jsx
<p className="text">ello, I am Joh</p>
```
if we set css like so:
```scss
.p {
	&::before {
		content: "H";
	}

	&::after {
		content: "n";
	}
}
```
In our page the sentence `Hello, I am John` will appear.

---
Categories: [[CSS]]
References:
