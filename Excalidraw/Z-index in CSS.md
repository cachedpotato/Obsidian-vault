---
tags:
---
# Z-index in CSS
The `z-index` is the CSS equivalent of `layer` in Photoshop, or any other drawing tools. the higher the index, the more to the forefront it is.
```css
.element1 {
	height: 20px;
	width: 10px;
	z-index: 1;
}

.element2_above_element1 {
	height: 20px;
	width: 10px;
	z-index: 2;
}
```
Z index also takes into consideration whether the element is nested or not. a nested element will NOT BE ABOVE A COMPLETELY UNRELATED ELEMENT WITH `z-index` HIGHER THAN PARENT:
![[context.webp|450]]


---
Categories: [[CSS]]
References:
