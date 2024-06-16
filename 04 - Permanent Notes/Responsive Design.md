---
tags:
---
# Responsive Design
Making sure our webpage looks good no matter what the platform is (whether it be PC, smart phone, tablet, etc.) is called having a _responsive design_. There are a number of elements to consider for responsive design, and these include:

- viewport
- media queries
- flexbox
- grids

## Viewport
Viewport is the visual part of the screen the user can actually see. It is clear that the viewport size of a PC screen is different from a viewport of a smart phone, so we must make our page adapt to different sizes. We can always just shrink our page in size and leave it at that, but that would make things ugly. Instead, what people do is add this simple line in HTML:
```HTML
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```
This line automatically adjust the width of our webpage for us.

## Media Queries
Media Queries is all about how our page is going to look depending on how we render it. We can create media queries with `@media`:
```HTML
<style>
	@media (min-width: 600px) {
		body {
			background-color: purple;
		}
	}
</style>
```

## Flexbox
If we have multiple elements we're trying to display on the same page at the same time, it might overflow. This affects mobile responsiveness, because if we just scale multiple elements down, it will become hardly visible. Instead, what we want is to freely wrap around these elements to fit in the mobile screen. Flexbox lets us do just that.
```HTML
<style>
	#container {
		display: flex;
		flex-wrap: wrap;
	}
</style>
```

## Grid
Besides flexbox layouts, there is also _grid_
```HTML
<style>
	#grid {
		display: grid;
		grid-row-gap: 20px;
		grid-column-gap: 20px;
		grid-template-column: 200px 200px auto;
	}
</style>
```



---
Categories: [[030-Web Development]], [[CS50 - Web Dev]]
References:
