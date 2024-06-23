---
tags:
---
# CSS Animation
We can add custom animations in CSS using the `@keyframes` property. As the name suggests, we can apply transformation, opacity change, or literally anything to a certain keyframe and create custom animation. Here's an extremely simple animation that makes an element blink:
```css
@keyframes blink {
	50% {
		opacity: 0;
	}

	100% {
		opacity: 1;
	}
}

.element:hover {
	animation-name: blink;
	animation-duration: 1s;
	animation-iteration-count: infinite;
	animation-timing-function: linear;
	animation-fill-mode: none;
}
```
Halfway through the animation, the element will become completely invisible. Then, at the end, it will be at full visibility (opacity 1). To call this animation, we can use the `animation-name` property.

## Properties
Speaking of properties, here are the list of properties related to animation:
- `animation-name`

- `animation-duration`

- `animation-delay`

- `animation-direction`: there are 4 options:
	- `forwards`
	- `backwards`
	- `alternate`: forwards then backwards
	- `alternate-reverse`: backwards then forwards

- `animation-iteration-count`: how many times the animation will be repeated.

- `animation-timing-function`: How the animation will transition from one keyframe to the other. options are:
	- `ease`: default. has that classic 'snapping' effect.
	- `linear`: linear transformation from a to b.
	- `ease-in`: slow start
	- `ease-out`: slow end
	- `ease-in-out`: slow start and end (`ease`)
	- `cubic-bezier`: custom values using the cubic bezier function
	
- `animation-fill-mode`: options for whether the element should retain values from a certain keyframe. Options are:
	- `none`: Animation will not apply any styles before OR after the animation
	- `forwards`: retains values set by the _LAST_ keyframe
	- `backwards`: retains values set by the _FIRST_ keyframe
	- `both`: follows rules for _BOTH_ first and last keyframes.

## Shorthand:
In order;
> animation: name duration timing-function delay iteration-count direction fill-mode

```css 
.anim_element {
	animation: blink 1s linear 0.3s infinite forwards forwards;
}
```


---
Categories: [[CSS]]
References:
