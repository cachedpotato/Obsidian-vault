---
tags:
---
# Hypertext Markup Language
Hypertext Markup Language, or _HTML_, is a _markup language_ for webpage aesthetics. It is not necessarily a computer language (a computer language implies that it's Turing complete which HTML definitely isn't) but it gets the job done.

HTML is a relatively simple language, and while mastering the art of HTML is hard, with the following two concepts (tags and attributes), we basically know all there is to HTML, and can actually make a functional (albeit ugly) webpage. Before we jump in, let's look at a very basic example of an HTML file:

```html
<!DOCTYPE html>
<html lang= "en">
	<head>
		<title>Hello, Title!</title>
	</head>
	<body>
		Hello, World!\n
		Hello, Body!
	</body>
</html>
```
To actually get this HTML file to serve as a webpage, we need to hook it up to a server. downloading `http-server` works fine too.
## Tags
tags are what comes fist right after the angular brackets. Using the example HTML file above, `html`, `head`, `title`, etc. are tags. tags always start with `<tag>` and ends with `</tag>`. Again, the HTML file above, we can see that the `<body>` contains the text, then it closes with `</body>`.
### Notable Tags
- `<meta>`: for metadata, such as name, size, encoding, etc.
Unlike other tags, `<meta>` doesn't require closing tags.
- `<title>`: for text we see for the tabs in the browser
- `<body>`: main body of the webpage
- `<p>`: paragraphs
- `<div>`: a division, or a rectangular portion, of the webpage
- `<h1>, <h2>...`: headers, the smaller the number suffix, the bigger the header
- `<ul>`: unordered list. Used in tandem with `<li>` (list item) to create bullet point-like lists.
- `<ol>`: ordered list. Uses numerals instead of just points.
- `<table>`: Tables. sub-tags are: `<tr>` for table rows, and `<td>` for table data.
```HTML
<!DOCTYPE html>
<html lang="en">
--snip
<body>
	<table>
		<tr>
			<td>1</td>
			<td>2</td>
			<td>3</td>
		</tr>
	</table>
</body>
</html>
```

- `<img src="path/to/image.png>`: Image. needs the `src` attribute to annotate the source image
- `<video>`: Video. The `<source>` tag is used in tandem for more fine-tuned video playback.
- `<a>`: an _anchor_ tag. most often used with `href` for hyperlinks.
## Attributes
Attributes are what comes after the tag, _within_ the angular brackets. attributes can also have values, often times in quotations. the `lang = "en"` above is an example of `attribute, value` pair.

### Notable Attributes
- `<meta>`: `name` , `content`, `width`, to name a few. The following lines of code is used traditionally for mobile compatibility:
```HTML
<meta name="viewport" content="initial-scale = 1, width = devide-width">
```
- `<video>`: `muted`, `control` for muting the video and adding sliders to the player respectively.
	- `<source>`: `src`, `type` for the source file of the video and the file type, respectively.
- `<a>`: `href` for hyperlinks.
```HTML
--snip
<body>
	visit <a href = "www.harvard.edu">Harvard</a>.
</body>
```
On the website, there will be a hyperlink in the word Harvard, and will direct to www.harvard.edu once clicked.

## Whitespace
HTML doesn't really care about whitespace bigger than length 1. To actually create paragraphs, use the `<p></p>` tag (the paragraph tag)

We can also divide our page into subdivisions with `<div>`.

## `data`
We can add some data to each HTML element with the attribute `data-name`. for example, if we want to store data about colors for our buttons:
```html
<button data-colors="red">Red</button>
<button data-colors="blue">Blue</button>
<button data-colors="green">Green</button>
```

We can then access this using `dataset.name` in JavaScript, like so:
```js
function stuff() {
	document.querySelectorAll('button').forEach(function() {
		document.querySelector('h1').style.color = 
			button.dataset.colors;
	})
}
```

---
Categories: [[040-Computer Network]], [[030-Web Development]], [[CS50 - Introduction]]
References:
Created: 2024-06-13
