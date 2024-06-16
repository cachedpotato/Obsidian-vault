---
tags:
---
# SASS
SASS is an extension of CSS to minimize redundancy in our code, using the concept of variables. the extension is `.scss` instead of `.css`
```css
ol {
	border: 10px solid red;
	font-size; 12px;
}
ul {
	border: 10px solid blue;
	font-size; 12px;
}
div {
	margin: 10px;
	font-size: 12px;
}
```
Here we can see that the `font-size` for all of the types above have `12px`. If we know we want all of this to be the same, changing these one by one can be a hassle. using SASS, we can just create a variable for this, and pass the name of the variable to the according property.

## SASS Variables
SASS uses `$` sign to indicate variables.
```SCSS
$font-size: 12px;
ol {
	border: 10px solid red;
	font-size = $font-size;
}
ul {
	border: 10px solid blue;
	font-size; $font-size;
}
div {
	margin: 10px;
	font-size: $font-size;
}
```
Now we just need to change one line for change font size for the selected types!

However, there is one small problem: browsers by default does not understand SASS. What we need to do, is download SASS, and using the following command, compile it and generate a CSS file:
```bash
$ sass variables.scss:variables.css
```
Here we create a CSS file `variable.css` from `variables.scss`. then we link this file into our HTML file.
Because we need to keep recompiling our file whenever we make changes, using SASS can be quite annoying. Thankfully, SASS provides this neat command `watch`, where it automatically compiles the SCSS file whenever it detects a change:
```bash
$ sass --watch variables.scss:variables.css
```

## SASS inheritance
like in OOP, SASS also provides inheritance. For example, given a type `message`, we can have "children" of this type using `class="success"`, `class="warning"`, etc. because all children of this message shares whatever's defined in the `message` type, it would be redundant to copy paste everything that's there to them. instead, we can inherit it using `@extend`:
```SCSS
%message {
	border-radius: 4;
	border: 3px solid black;
	font-size: 20px;
}
.success {
	@extend %message;
	background-color: green;
	font-family: arial, sans-serif;
}
.warning {
	@extend %message;
	background-color: red;
}
```


---
Categories: [[CSS]], [[CS50 - Web Dev]]
References:
