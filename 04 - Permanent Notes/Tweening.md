---
tags:
---
# Tweening
Tweening is a game development term for interpolation. Through tweening, we can change a value (or property) of something into the other, within a given timeframe. For example, When we collect coins, we can add a cool little animation sequence that makes the coin grow in size as it disappears, to really sell that the player obtained this coin. A crude pseudocode would go something like:

```
var time = t;
timer start()
some_value = time_elapsed* some_other_value 
	+ some_value(time - time_elapased)
timer end()
```
This is a super simple interpolation process using the parameter `t` and the formula $y = t*x_2 + (1 - t)*x_1$. as t moves towards 1, the point will move from $x_1$ to $x_2$. 

![[Pasted image 20240614150415.png]]

Now let's look at an actual example (the coin example) in Godot.
```GDScript
func pickup():
	$CollisionShape2D.set_deferred("disabled", true);
	var tw = create_tween().set_parallel().set_trans(Tweem.trans_QUAD);\
	tw.tween_property(self, "scale", scale * 3, 0.3)
	tw.tween_property(self, "modulate:a", 0.0, 0.3)
	queue_free()
```
first we create a variable `tw`, which is called a `tween object`, and set it so that tweening process happens in parallel.
Next, we actually tween properties that we want, which are:

- scale: in 0.3 seconds, increase the size 3 times
- `modulate:a`: change the opacity to 0 in 0.3 seconds

Setting the opacity to 0 will make it transparent. After all is done, we delete the coin instance with `queue_free()`. 


---
Categories: [[Game Development]], [[CS50 - Game]]
References:
