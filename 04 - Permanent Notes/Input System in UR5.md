---
tags:
---
# Input System in UR5
Unreal Engine's Input system is quite robust, to say the least. We first need to create what's called an "Input Context", then hook that to our player which in and of itself takes multiple steps. Let's start with Input Action and Input Context.

## Input Action and Input Mapping Context
An input action is the smallest element of input in Unreal Engine. It has properties like description, Triggers, Modifiers, etc. An Input Mapping Context is a collection of input actions, and can assign key bindings.
![[Pasted image 20240622005031.png|600]]
The pictogram above shows the basic flow of getting inputs. We create Input actions, which makes up an input mapping context. Then, we insert this into our player blueprint.

## Importing IMC from player blueprint
We can't just get the IMC and hook that directly to `Event BeginPlay`. In fact, it's rather complicated:
![[Pasted image 20240622010035.png]]

First, we need to possess the player. We can do it in 2 ways:
- From the main menu, select `Basic > Player Start`, and add that to the player
- From the Event Graph, Connect `Event Begin Play`, `Get Player Controller`, and a reference to `self` to `possess` node.
Then, we cast that to `PlayerController`, Pass that through what's called an `Enhanced Input Local Subsystem`, and then we can hook that to `Add Mapping Context` node.

### Enhanced Input Local Subsystem

## Possessing the character
We've looked at a basic example of how to possess a player object above, so let's now look at a more general way of doing this.

1) In the Game Mode blueprint, set the `default pawn class` to the player blueprint
2) Under project settings, change the default game mode to the game mode blueprint we just created.
3) In the player blueprint, cast the game mode to our custom Game Mode blueprint.
![[Pasted image 20240628183830.png]]
5) In the main editor, create a new `PlayerStart` instance. It looks invisible at first, but when we test play, we can see the sprites are loaded up correctly.
6) Now all we have is the camera. We want the camera follow the character as it moves along so we need two things:
	- a `spring arm` to attach the camera to
	- the camera itself
We can set it inside our player blueprint.
![[Pasted image 20240623131559.png]] ^cb5ba8
5) Rotate the spring arm in the Y axis by negative 90 degrees. The camera should be facing the player now.
6) Depending on the game we're making, we may want to disable `collision check` on the spring arm, as it can clip to collision boxes.


---
Categories: [[Unreal Engine]]
References:
