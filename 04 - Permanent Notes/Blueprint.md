---
tags:
---
# Blueprint
Blueprint is the signature feature of Unreal Engine, and is a visual scripting method for game development. instead of writing code, we can create nodes and connect them together for creating in-game logic.

Blueprints are great at light-weight stuff and is easy to use, at the cost of some performance. Using C++ will result in better performance, but because it's well, C++, it may hinder development time. Generally it's advised to have a healthy mix of both.

Naming conventions for blueprints are simple: prefix the blueprint files with `BP_`, ex) `BP_PlayerMovement`, `BP_Pickup`, etc.

The "Blueprint" portion of the Blueprint file can be accessed in the "Event Graph" section.

## Basic Structure of Event Graph Node
![[Pasted image 20240621231350.png |630]]
- White Arrows: Execution Flow. Will execute from left to right.
- Green Nodes: Input/Return Values
- Pink Nodes: Converted Inputs/Return Values

Here we get our 'Elapsed Time' variable that tracks how much time has passed, and [[Delta Time]]. We add that using the `add` node, then pass it to `Set Elapsed time` event node, which we hook the output to `Print String`. In short, we're trying to print how much time has passed into the screen. In C++ Terms:
```C++
#include <string>
std::string print_time(int& delta, int& ElapsedTime) {
	ElapsedTime += delta;
	return ElapsedTime.to_string();
}

```


## Event Graph Basics
At the start, there will be some default nodes such as:
- `Event BeginPlay`
- `Event ActorBeginOverlap`
- `Event Tick` 

1) `BeginPlay`
Activates only once when the game is initialized or when the player is spawned. Used for spawning objects, putting ammo into guns, etc.

2) `Tick`
Called _EVERY SINGLE FRAME_ when the player is active. Used for dynamically changing the speed of an object, tracing objects, etc.

3) `ActorBeginOverlap`
Not used often. We can select other options such as `OnComponentBeginOverlap` instead.

Other useful Events will be listed [[Useful Nodes in Event Graph|here]]. 

## Variables
As Event Graph is an "alternative" for base C++ codes, it also has the ability to store variables. On the right tab, we can create new variables, and by compiling we can set their default values. available types are based on C++ types.

Drag it onto the Event graph, and you'll get two options:
- `GET <variable>`: for getting (hooking) the value for other nodes.
- `SET <variable>`: for changing its value

ex) HOOK `GetWalkSpeed` > `GET MySpeedVariable` > `+` > `SET MaxWalkSpeed`
This will increase the max walk speed by the variable value.

One cool thing about variables is that by clicking `instance editable` option, we can create the identical instance with different value stored in the variable.

## Functions
Just like Any other programming language, you can also create custom functions and add that freely to our event graph where we see fit. We can add inputs by clicking the `inputs` option on the right. 


## Useful tips
- Clicking the `ALT` key will remove edges.
- Double clicking on the edges creates a "reroute" where you can hook different things with. You can also move this around.
- `Q` aligns node in a horizontal axis






---
Categories: [[Unreal Engine]], [[020-Game Development]]
References:
https://dev.epicgames.com/documentation/en-us/unreal-engine/recommended-asset-naming-conventions-in-unreal-engine-projects?application_version=5.2

