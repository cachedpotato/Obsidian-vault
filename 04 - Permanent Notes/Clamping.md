---
tags:
---
# Clamping
Clamping is used to limit the range of positions at which the player, or any object, can be. Even if the user inputs `right`, there must be some sort of mechanism to make the player not be able to go further than intended.

While yes, collision detection can be used in walls to prevent this from happening, what we're talking about here is more about going _off screen_. Clamping is what solves this problem. Of course, How clamping is implemented will differ from engine to engine, but here's an example in Godot:

```Godot
var screensize: Vector2 = Vector2(480, 720)
func _process(delta):
	velocity = Input.get_vector("ui_left", "ui_right", "ui_up", "ui_down")
	position = position + velocity * SPEED * delta;

	#clamping
	position.x = clamp(position.x, 0, screensize.x)
	position.y = clamp(position.y, 0, screensize.y)
```

*After* calculating the position, we `clamp` it to some boundary, which in this case is the size of the screen defined by the `scrensize` variable.

---
Categories: [[Game Development]]
References:
Created: 2024-06-14
