---
tags:
---
# CSS ID and Class
Say we have some CSS code that defines how we should style our `h1` headers.
```CSS 
h1 {
	color: rgb(244, 103, 123);
	border: 5px solid black;
	border-radius: 4;
}
/*...
```
This will apply to ALL the `h1` headers. what if we need a different style for one of these headers? Here, we can utilize `id`s. Just like how IDs are unique identifiers in real-life, it's best to make IDs unique.
```HTML
<body>
	<h1>Table</h1>
	<table>
		<tr><td>1</td><td>1</td><td>1</td></tr>
		<tr><td>1</td><td>1</td><td>1</td></tr>
		<tr><td>1</td><td>1</td><td>1</td></tr>
	</table>
	<h1 id = "description">Description </h1>
	<div>Lorem Ipsum</div>
</body>
```
here, we assigned an ID `description` to just one of our headers. to style this in CSS, we use the `#` symbol:
```CSS
h1 {
	border: 5px solid black;
	margin: 10px;
}

#description {
	border: 1px solid green;
	border-radius: 2px;
}
```
When it comes to [[Specificity in CSS|specificity]], `id`s will come first, so the `h1` styling will be ignored.

ID are mostly for one-off styling only. Then what if we want to style a certain subset of the same tag? we use what's called as a class.
```HTML
--snip
<div>This is a text. This goes pretty long</div>
<div>This is a text. This goes pretty long</div>
<div>This is a text. This goes pretty long</div>
<div class= "big"> This is a text. This goes pretty long</div>
<div class= "big"> This is a text. This goes pretty long</div>
<div class= "big"> This is a text. This goes pretty long</div>
```
in CSS, we can add stylings for class with the `.` symbol, followed by the class name:
```CSS
.big {
	font-size: 14px;
	font-family: FiraCode, Arial
	text-align: center;
}
```


---
Categories: [[CSS]] , [[CS50 - Web Dev]]
References:
