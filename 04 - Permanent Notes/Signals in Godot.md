---
tags:
---
# Signals in Godot
Signals are used to define behavior of a node when a certain situation happens. Some signals are built in, meaning just by creating a node, you can use it just by connecting it to something, or you can create one entirely, like this:
```godot
signal pickup #for picking coins
signal hurt #when the player is hurt
```

When you connect a signal to a node, a new function is created in the form of `_on_node_name_signal_name`, for example:
```
func on_player_pickup():
	pass
```
will be created when we connect the pickup signal to the `Player` node. Let's create a more sophisticated example. This is what we're gonna do:

- If the player's collision box reaches a coin's, it will emit the pickup signal
- If the player's collision box reaches an obstacle's it will emit the hurt signal and promptly die.
``` godot
func _on_area_entered(area):
	if area.is_in_group("coins"):
		area.pickup()
		pickup.emit()
	if area.is_in_group("obstacles"):
		hurt.emit()
		die()
```
the `area.pickup()` method is a function defined somewhere else - `coins.gd` in this case, which defines what coin does when it gets picked up. We can also see that here, we got a signal, and depending on what we hit, we emit two different signals - `pickup` or `hurt`. this can be used somewhere else, say in the `main` node like so:
``` godot
func _on_player_pickup():
	score += 1
	$HUD.update_score(score)
	$CoinSound.play()

func _on_player_hurt():
	$EndSound.play()
	game_over()
```



---
Categories: 
References:
Created: 2024-06-02
