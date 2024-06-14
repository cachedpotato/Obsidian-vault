---
tags:
---
# Specificity in CSS
Because we can define stylings by id, class, type, etc, there may come a time where the styling conflicts with each other, like so:
```CSS
#foo {
	border-radius: 10;
}
table {
	border-radius: 15;
}
```

```HTML
<table id="foo">
	<tr>
		<td>Hello</td>
		<td>There</td>
		<td>Buddy!</td>
	</tr>
	<tr>
		<td>I</td>
		<td>Am</td>
		<td>John</td>
	</tr>
</table>
```
Here, the `table` has `id = foo`, but in CSS, the border radius size are set differently. In this case, CSS will follow the one with more _specificity_. the order of specificity is as follows

- inline: literal `style = ""` element inside the HTML file
- id
- class
- type: think of these as tags

because id has higher specificity than table, it will follow the `#foo` style guide.

## selectors
Besides ID and class, we can use selectors for getting the subset of HTML that we want, and these include:

| selector | Description               |
|:--------:|:------------------------- |
|   a, b   | Multiple Element Selector |
|   a b    | Descendent Selector       |
|  a > b   | Child Selector            |
|  a + b   | Adjacent Sibling Selector |
| \[a=b\]  | Attribute Selector        |
|   a:b    | Pseudo-class selector     |
|   a::b   | Pseudo-element selector   |
```HTML
<ol>
	<li>list item one</li>
	<li>list item two</li>
	<li>list item three</li>
	<ul>
		<li>list item four</li>
		<li>list item five</li>
	</ul>
</ol>
```

```CSS
ul > li {
	color: green;
}
```
This will only change color for list items under the unordered list entity.




---
Categories: [[CSS]] , [[CS50 - Web Dev]]
References:
