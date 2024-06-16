---
tags:
---
# 2D Coordinate Convention for Games
2D coordinates for gaming has one unique difference than our normal use case of Cartesian coordinates, in that the y axis is flipped. Meaning, the positive y values go DOWNWARD, and negative y means we're going UP:
![[Pasted image 20240614033132.png|450]]

Besides this y axis flip, everything remains the same. I mean, it's just a cartesian coordinates after all. the formula:
$$
(x_{i+1}, y_{i+1}) = (x_{i}, y_{i}) + (dx, dy)
$$
remains the same for position calculation, where $i, i + 1$  are frame numbers. a code implementation would look something like this:

```GDScript
var SPEED: int = 200;

func _process(delta):
	velocity = Input.get_vector("ui_left, ui_right, ui_up, ui_down");
	position += velocity * speed * delta
```
here the `velocity * speed * delta` is the $(dx, dy)$ part of the formula. this update is done every frame. We can also see here that the direction in which the object will move is represented as the vector created by user's keyboard input.

---
Categories: [[020-Game Development]], [[CS50 - Game]]
References:
Created: 2024-06-14
