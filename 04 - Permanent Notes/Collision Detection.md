---
tags:
---
# Collision Detection
For 2D games, sprites are what appears on the screen, whether it be an inanimate object, a background, the player, etc. However, sprite is just an image. We need some sort of mechanism for these objects to react to various environmental cues. For example, when our player sprite _gets hit by_ an enemy, the player will lose health. How do we define if something got hit?

Game developers call this _collisions_. Collisions happen when two different _boxes_, that we've assigned to each object, _INTERSECTS_ with one another. These boxes are called **collision boxes**, and is a _SEPARATE ENTITY_ from the sprite and sprite size:
![[aS5dVfx-2318253157.png]]
Here we can see the character models and a bunch of boxes. Fighting games are DEFINED by these boxes, and if you tear it down into the most basic elements, fighting game is a sequence of the following:
1) user input generates some hitbox (collision box)
2) if this hitbox _COLLIDES_ with the other player's hurtbox (another type of collision box), the other player takes damage

Hitboxes are shown in yellow, and hurtboxes are shown in green in the image above. We can see that they do not necessarily match exactly with the model. In fact, the hitbox of Ken's punch far extends beyond his arm length. Because collision boxes are independent of sprites, we can have as much fun as we want with it.

## When do Collision Boxes 'Collide'?
Collision boxes are cool and all, but it must do its job, which is:
- if collision box _collides_ with another collision box, do some logic
How do we define collision then? well, it's pretty straightforward.
![[Pasted image 20240614102308.png|500]]
Given two collision boxes A and B, with its leftmost coordinates and their respective width and height value, collision happens when:
1) The upper right corner of A is at the left of B
2) The upper left corner of A is at the left of B
3) The lower left corner of A is at the left of B
4) The upper left corner of A is above upper left corner of B

This is known as the _AABB_ algorithm.
In code, it would look something like this:
```lua
if (A.x + A.width) >= (B.x) && (A.x) <= (B.x + B.width) then
	if (A.Y + A.Height) >= B.y && A.y <= (B.y + B.height) then
		collision = true
	end
end
```
This is quite the long line of code just for collision detection. Most game engines will have a method for its `collision box` class, such as the case in Godot:
```GDScript
func _on_area_entered(area):
	if area.is_in_group("coins"):
		area.pickup()
	elif area.is_in_group("obstacles"):
		hurt.emit()
		die()
```


## Advanced Collision Detection mechanism for game engines
Game engines, such as [[Collision Detection related settings in Unreal Engine|Unreal Engine]] or [[Collision Detection System in Godot|Godot]] offer more than just having a collision box and bare-bones detection mechanism. For example in Unreal engine there are a plethora of events related to how the Collision box interacts to other object types, such as `On Event Begin Overlap` or `On Event Hit`.



---
Categories: [[020-Game Development]], [[CS50 - Game]]
References:
Created: 2024-06-14
