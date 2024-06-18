---
tags:
---
# CSS Quirks
Here are some notable classes in CSS
## `input`
this corresponds to `<input type = "sth">` in html.
```css
input[type="color"] {
	border-radius: 25px;
	width: 75px;
	height: 50px;
	padding: 5px;
}
```

## transition
For setting transition properties
```css
.color_display{
	display: flex;
	justify-content: center;
	align-items: center;
	transition: 0.25s ease;
}
```

## list and margins
For some reason setting padding to 0 gets rid of the numbers in ordered list items?
```css
ol {
	padding: 0;
}
li {
	align-items: center;
	display: flex;
}
```

## `backdrop-filter`
This is used to add graphical effect such as `blur` _BEHIND_ the element.
```css
.clock-container {
	backdrop-filter: blur(5px);
}
```

## Graphical Effects
Speaking of, here are some of the graphical effects native to CSS
- `blur(px)`
- `sepia(%)`
- `invert(%)`

---
Categories: [[CSS]]
References:
