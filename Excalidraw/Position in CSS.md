---
tags:
---
# Position in CSS
The `position` property in CSS is normally used for child elements' position and its relation to its original position. There are 6 possible values:
- relative
- absolute
- fixed
- sticky
- static
- inherit

The first two are the most commonly used, and the rest have their own quirks. Here are brief explanation for the first 4 (I'll get to the latter 2 if I find a need to use it myself)

## Relative
`relative` here means the `top/down/left/right` properties will apply _relative to its original position_. 
```css
.element {
	position: relative;
	top: 10px;
	left: 15px;
}
```
Compared to its relative position, the above CSS will shift the element down by 10px and right by 15px.

## Absolute
`absolute` positioning here means that the `top etc.` properties will follow in relation to the _DOCUMENT_, and has no relations with the original position:
```css
.element {
	position: absolute;
	bottom: 0
}
```
this will place the element at the bottom of the document.
if we want _absolute_ placement _relative_ to its parents, we must set the parent's position to `relative`:
```scss
.parent {
	position: relative;
	.child {
		position: absolute;
		bottom: 0;
	}
}
```
This will place child element at the bottom of the parent element.

## Fixed
Quite similar to absolute, except for the fact that it's not related to the document as well. Rather, it's positioning can be thought of as based on the "monitor/screen", meaning, it will _ALWAYS STAY ON SCREEN_.
```css
.hes_just_standing_there_menacingly {
	position: fixed; 
	left: 15px;
	top: 20px;
}
```

## Sticky
A mix between relative and fixed, and when it changes is based on scrolling. `sticky` fist start as a `relative` position, but when the user scrolls past its normally visible area, it would stick to the location set by placement properties:
```css
.sticky_bar_h {
	position: sticky;
	top: 0px;
	display: block;
	content: 'WHAAAAAAAAAAAAAAAAAAAA'
}
```
This element will `stick` to the top of the screen once the document's been scrolled down enough. This can be really useful for something that's good to be on screen all the time, live navigation bars.

## Placement Properties
What I mean here are these 4 properties
- top
- bottom
- left
- right
As explained above, these are closely related to positional properties. It acts quite similar to margins, except that this is not really related to the box model (so in relation to other elements). This is purely for position shifting.

If these values are set to some positive value, the element will move to the opposite side by that value. For example, 
```css
.move_down {
	position: relative;
	top: 10px;
}
```
will move _DOWN_ this element by 10px. The cool thing about this is that we can set these values to a negative number:
```css
.we_going_up {
	position: relative;
	top: -10px;
}
```
this will move the element _UP_ by 10px.



---
Categories: [[CSS]]
References:
