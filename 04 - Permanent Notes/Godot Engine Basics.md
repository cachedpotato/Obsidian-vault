---
tags:
---
# Godot Engine Basics
Godot Engine's main schtick is that everything is interpreted as a tree of [[Nodes in Godot|nodes]], and that tree is called a scene. A scene doesn't necessarily mean a "dramatic" scene you see in movies, it's just an instance of something, such as a Player character.

A very basic player character example will consist of 3 notes:
```
Area2D (the root node)
	- AnimationSprite2D
	- Collision2D (For Collision Box)
```
We can set the animation sprites (idle, run, hurt, etc) within the `AnimationSprite2D` node, and set its Collision Box in the `Collision2D` node.

However, that is definitely not all - we must apply logics to the character!
Godot Engine uses two languages: GDScript and C Sharp. GDScript is surprisingly fast given how high-level it is (it's basically like python) due to its extremely close connection with the low-level base engine, which is made in C++. An example of A player movement script would be something like this:

``` godot
@export var speed = 350
var velocity = Vector2.ZERO
var screensize = Vector2(480, 720)

signal pickup
signal hurt

func _process(delta):
	#x neg, x pos, y neg, y pos
	velocity = Input.get_vector("ui_left", "ui_right", "ui_up", "ui_down")
	position = velocity * speed * delta

	#add limit
	position.x = clamp(position.x, 0, screensize.x)
	position.y = clamp(position.y, 0, screensize.y)

	#animations
	if velocity > 0:
		$AnimationSprite2D.animation = "run"
	else:
		$AnimationSprite2D.animation = "idle"

	#flip sprites if x is negative:
	if velocity.x != 0:
		$AnimationSprite2D.flip_h = velocity.x < 0
```

Few things to note here:
1) functions that start with `_` are often related to [[Signals in Godot|signals]] and/or related to just base logic of the node. the `_process` function shown here is for logics process _every frame_ another example is `_ready` which is a function run _once_ when the node is first instantiated.

2) the `$` sign is for calling the nodes directly. As seen from the player node above, it has a node `AnimationSprite2D` that contains the animation data, as well as methods and variables that can be called within the GDScript, for example, the `animation` or `flip_h` (for flipping sprite).

3) GDScript by default is _dynamically typed, but static typing is possible._ 

Add a bunch of scenes together, add logics, and voila, your game is done. Super simple, right?

...right?
## Cases
There seems to be an internal case rules in Godot which are the following:

1) variables, function names are in `snake_case`
2) Nodes are in `PascalCase` 
3) Directories are in `snake_case`





---
Categories: [[020-Game Development]] [[Godot Engine]]
References:
Created: 2024-06-02
