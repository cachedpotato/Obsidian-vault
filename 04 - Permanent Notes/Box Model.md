---
tags:
---
# Box Model
![[CSS-Box-Model-4099676731.png]]
CSS lets us fine-tune spacing of contents. By dividing the spaces between the content, border, and external elements, we get this onion-like structure, which is called the box model. Definitions are as follows:
- Margin: Space outside of the border.
- Border: The "final" layer that encloses our content
- Padding: Space _inside_ the border, but _outside_ our actual content.

We can set margin and padding using 1 ~ 4 values:
```CSS
div {
	margin: 10px 10px 15px 15px;
	padding: 10px 5px;
}

a {
	margin: 1px;
	padding: 5px 10px 5px; 
}
```

- 4 numbers: top right bottom left
- 3 numbers: top (right & left) bottom
- 2 numbers: top & bottom right & left
- 1 number: all sides

We can split and specify exactly which side we're setting like this:
```CSS
div {
	margin-top: 10px;
	margin-right: 10px;
	margin-bottom: 15px;
	margin-left: 15px;
}
```

## A bit more on borders
while margin and paddings define space/area between thigs, border is just...Border. However, that does not mean we can't do cool things with it:
```CSS
div {
	border: 5px solid black;
	border-radius: 3;
}
```
`border-radius` changes the roundness of border edges, with `100` being the max value (complete circle).


---
Categories: [[CS50 - Web Dev]], [[CSS]]
References:
