---
tags:
---
# Animations in HTML using CSS
HTML doesn't just support cool borders and images, it also supports animations! Below is a simple animation that makes our header grow in size:

```HTML
<!DOCTYPE html>
<html lang="en">
	<head>
		<title>Animation</title>
		<style>
			@keyframes grow {
				from {
					font-size: 12px;
				}
				to {
					font-size: 200px;
				}
			}

			h1 {
				animation: grow; 
				animation-duration: 2s;
				animation-fill-mode: forward;
			}
		</style>
	</head>
	<body>
		<h1>Welcome!</h1>
	</body>
</html>
```
Here we declare a keyframe `grow` which will increase a part of our page, in this case the header. We first declare how the animation is going to work with `@keyframes grow`, then after that we actually implement this in our `h1` with `animation: grow;`. We can also set other variables such as `animation-duration` and `animation-fill-mode`.

## Keyframes
In the above example, `@keyframes` uses 2 attributes `from` and `to`. whatever we're trying to animate, define how one thing turns `from` something `to` something. However, we can do much more than this with `%` the `%` describes how far into the animation we're in, in terms of percentage. Now that we know we have a lot more control in our animations, we can go hog wild:

```css
@keyframes rad {
	0% {
		font-size: 12px;
		left: 0%;
		border-radius: 0;
	}

	50% {
		font-size: 100px;
		left: 50%;
		border-radius: 20;
	}

	75% {
		font-size: 50px;
		left: 65%
		background-color: red;
	}
	100% {
		font-size: 12px;
		left: 0%;
		border-radius: 0;
		background-color: blue;
	}
}

h1 {
	position: relative;
	animation: rad;
	animation-duration: 4s;
}
```

## Animation Properties
We can also define other aspects of animation with animation properties. Here are some notable examples:
- `animation-duration`: pretty self explanatory I think.
- `animation-iteration-count`: repetition count for animation
- `animation-fill-mode`: option for whether the element should retain the last value of the keyframe. `forward` is true.
- `animation-play-state`: whether the animation is `paused` or `running`


## Controlling Animation with JavaScript
Like any other CSS elements, we can interact with them with JavaScript. the "ON/OFF" switch of the animation can be accessed by `element.animationPlayState`. This value can be either `paused`, meaning the animation isn't playing and `running` meaning it is. Now let's add a simple switch to our animation:
```js
document.addEventListener('DOMContentLoaded', () =>{
	const h1 = document.querySelector('h1');
	h1.style.animationPlayState = 'paused';
	document.querySelector('button').onclick = () => {
		if (h1.style.animationPlayState === 'paused') {
			h1.style.animationPlayState = 'running'; 
		} else {
			h1.style.animationPlayState = 'paused';
		}
	}
}) 
```

We can also create a cool animation that removes a post from a chunk gradually, like so:
```js
document.addEventListener('DOMContentLoaded', () => {
	document.addEventListener('click', event => {
		const event = event.target;
		if (event.className == "hide") {
			//remove content
			event.parentElement.style.animationPlayState = 'running';
			event.parentElement.addEventListener('animationend' () => {
				event.parentElement.remove();
			});
		}
	});
});
```

```html
<style>
	@keyframes hide {
		0% {
			opacity: 1;
			padding; 20px;
			margin: 10px;
		}
		/*make it invisible first*/
		75% {
			opacity: 0;
			padding; 20px;
			margin: 10px;
		}
		/*decrease its size to create a "sliding up" like animation*/
		100% {
			opacity: 0;
			height: 0;
			line-height: 0;
			padding: 0px;
			margin: 0px;
		}

		.post {
			animation-name: hide;
			animation-play-state: paused;
			animation-duration: 2s;
			padding: 20px;
			margin: 10px;
		}
	}
</style>
```

---
Categories: [[030-Web Development]], [[CS50 - Web Dev]]
References:
