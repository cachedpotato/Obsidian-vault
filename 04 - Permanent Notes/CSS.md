---
tags:
---
# CSS
CSS is a "language" made for designing webpages. While this seems to be doing the same thing as [[Hypertext Markup Language|HTML]], it actually complements what HTML does. If HTML contains the basic layout and the actual bodies of text and images that goes into a webpage, CSS is purely about design and aesthetics. We can import our CSS files in our HTML file like so:

```HTML
<!DOCTYPE html>
<html lang="en">
	<head>
		<link href = "style.css" rel="stylesheet">
	</head>
</html>
```

## Why CSS?
CSS stands for _Cascading Style Sheets_. What exactly do we mean by Cascading? Consider the following HTML styling for example:
```HTML
<html lang="en">
	<head>
		<title>mytitle</title>
	</head>
	<body>
		<div style = "align: center; fontsize=big;">square1</div>
		<div style = "align: center; fontsize=medium;">square2</div>
		<div style = "align: center; fontsize=small;">square3</div>
	</body>
</html>
```
To align all divisions, using normal HTML styling methods we had to put `align: center` on each division. Why can't we just, idk, add it to the body?
```HTML
--snip
<body stype = "align: center;">
	<div style = "fontsize=big;">square1</div>
	<div style = "fontsize=medium;">square2</div>
	<div style = "fontsize=small;">square3</div>
</body>
```
much better! see how the `align: center` _cascaded_ through the entire body? CSS can be thought of as a collection of key-value pairs of styling, to cascade that styling to all of the needed paragraphs/divisions.
## Basics of CSS
Whatever's inside the `<style>` tag, that's the actual code of CSS. a very simple CSS code would look something like this:
```CSS
#harvard {
	color: green;
}

#yale {
	color: blue;
}

a {
	color: red;
}

a:hover {
	text-decoration: underline;
}
.big {
	font-size: 13;
	align: center;
}
.medium {
	font-size: 12;
	align: center;
}
.small {
	font-size: 10;
	align: center;
}
```
the `a` here represents the tag `a` in HTML file. this means that whenever the anchor tag is used, the color of the text will be red.
We can see that we also have `a:hover` property. This applies to anchor tags _ONLY WHEN THE CURSOR IS HOVERING OVER THE TEXT_. we can add this kind of additional conditions with `:`.

We can also add stylings based on the `id` attribute. in CSS, The prefix `#` means this is the styling for id of the name that follows after the bang symbol. In this case,
```HTML 
<a href="harvard.edu" id = "harvard">Harvard</a>
```
means the text will now be in green, not red!

`.big` and the stuff that starts with `.` are _classes_ that we defined, which are just sets of properties. we can use this class anywhere we want within the HTML file using the `class` attribute:
```HTML
<div class="big">This is Big</div>
<div class="medium">This is Medium</div>
<div class="small">This is Small</div>
<a href = "www.google.com">Google</a>
```

---
Categories: [[030-Web Development]], [[CS50 - Introduction]]
References:
Created: 2024-06-14
