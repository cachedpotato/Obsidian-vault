---
tags:
---
# CSS Flex
Flex takes care of screen size issues, and dynamically rearrange things as the viewport dimension changes. We can enable flex in CSS using `display: flex`. Here are some notable features of flex:

## `flex: 1`
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

## `flex-direction`






---
Categories: [[CSS]]
References:
