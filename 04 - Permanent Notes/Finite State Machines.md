---
tags:
---
# Finite State Machines
Players, NPCs, or anything really, can be in multiple states. We can set flags to trigger each state. For example, when a player gets hit, we might want to put the player in a temporary "invulnerable" state, which can be triggered by the "hit" flag, and after the "timeout" flag for the invulnerable state is triggered, the player's invincibility stops. But what happens if multiple flags are triggered? how will we set the instance's state then? The simplest answer is to restrict anything to be in a single state only. This can be represented by what's called as a Finite State Machine (FSM).
![[FSM 2024-06-02 19.01.22.excalidraw.png]]
Above is a simple FSM for a Player. States are the ellipses. Text written on the arrows are the flags that trigger a transformation from one state to the other. We can see that There can be only one possible state at any given time, no matter how the flags are set.

Using States, we can control the player or game objects in a more modular fashion, keeping the code and logic cleaner than if we were to add arbitrary flags to everything.

In Godot, we can represent this using Enums as states.
```godot
enum {INIT, ALIVE, DEAD, INVULNERABLE}
```

## Updating states
FSM is useless unless we incorporate some way of changing states based on what the player does. There are many ways of implementing this, but one of the more simple approach is the following
- create a `change_state()` function that holds some sequence of logic to do when something is in said state.

- For any given object that can inherit this state, have them call this function whenever some flag is triggered.

A simple example of this in Godot would look like this:
```GDScript
signal lives_changed
func change_state(new_state):
	match new_state:
		INIT:
			$CollisionShape2D.set_deferred("disabled", true)
			#some other logic...
		ALIVE:
			$CollisionShape2D.set_deferred("disabled", false)
			#some other logic...
		DEAD:
			$CollisionShape2D.set_deferred("disabled", true)
			#some other logic...
		INVULNERABLE:
			$CollisionShape2D.set_deferred("disabled", true)
			#some other logic...


#--snip
func set_lives(value):
	lives = value
	lives_changed.emit(lives)
	if lives <= 0:
		change_state(DEAD)
	else:
		change_state(INVULERABLE)
```

Here we first define the `change_state` function, that mainly deals with collision detection. Then, in `set_lives` function, when lives is the value of 0, then we triggered the flag (see the FSM above) to change the player's state to `DEAD`, so we call the `change_state(DEAD)` function. This will disable the collision box.


---
Categories: [[020-Game Development]], [[CS50 - Game]]
References:
Created: 2024-06-02
