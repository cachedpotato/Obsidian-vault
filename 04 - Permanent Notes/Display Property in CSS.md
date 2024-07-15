---
tags:
---
# Display Property in CSS
There's a lot of display properties, including `flex` and `grid`. let's get into each and every one of them.

## Flex
Flex  dynamically rearrange things as the viewport dimension changes. We can enable flex in CSS using `display: flex`. Here are some notable features of flex:

### `flex: 1`
setting `flex` to some arbitrary value is a shorthand way of doing the following:
```css
.text {
	flex-grow: 1;
	flex-shrink: 1;
	flex-basis: 1;
}
```
- `flex-grow`: specifies the growth factor of the item
- `flex-shrink`: specifies the shrink factor of the item
- `flex-basis`: specifies the initial length of the item

Setting a flex item's `flex` to 1 means it will always take up as much space as possible within the flex container.

### `flex-direction`
Defines how the flex items are placed in the flex box.
- row: row-wise, left to right
- row-reverse: row-wise, right to left
- column: column-wise, top to bottom
- column-reverse: column-wise, bottom to top

### `justify-content`
Defines the alignment along the main axis. Justification normally sets the "end point" of an element (at least that's how I understand this). For example, `flex-start` will mean the first flex item will be at the very starting point. and if it's set to `space-between`, then both first and last element will be at their respective starting/end points. there are 6 values available:
- `flex-start` 
- `flex-end`
- `center`
- `space-between`
- `space-around`
- `space-evenly`

### align-items
![[align-items.svg | 300]]
Note that center means it's centered in the _non-main_ axis. What I mean is, the picture above is placed row-wise, so the `center` here means the center of the _column_ (height). 

### align-content
similar to `align-items` but this time for flex box with the number of items large enough to have "lines" between items (there are more than 1 row/column of items). Available values are the same with `justify-content`


## Grid
While 'Flex' gives, well, flexibility when it comes to placement, the `grid` display option is a little more strict. as the name suggests, it places the contents on a grid, and how much space every content occupies is set with the `grid-template-areas` property:

```css
.item1 { grid-area: header; }
.item2 { grid-area: menu; }
.item3 { grid-area: main; }
.item4 { grid-area: right; }
.item5 { grid-area: footer; }

.grid-container {
  display: grid;
  grid-template-areas:
    'header header header header header header'
    'menu main main main right right'
    'menu footer footer footer footer footer';
  gap: 10px;
  background-color: #2196F3;
  padding: 10px;
}
```
![[Pasted image 20240621001840.png|500]]
Here we see we made a 3 x 6 grid display. we can merge each cells together for a single component by placing which `grid area` is supposed to occupy each cell. For example, the `header` takes all 6 cells in row 1, so it's repeated 6 times.

## Block and inline
Setting the display property to `block` will make that element take up the _entire width_ of the container. Contrast to this, `inline` takes up only the amount of space it's actually required, and will not push other elements away to make space. Meaning, it can overlap with other elements.

inline elements include:
- `<img>`
- `<button>`
- `<strong>`
- `<input>`
- `<textarea>`




---
Categories: [[CSS]]
References:
https://css-tricks.com/snippets/css/a-guide-to-flexbox/
https://www.w3schools.com/css/css_grid.asp