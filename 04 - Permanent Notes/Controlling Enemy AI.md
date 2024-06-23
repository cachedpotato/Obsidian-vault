---
tags:
---
# Controlling Enemy AI
NPC/Enemy controls is a HUGE part of Enemy AI. [[Useful Nodes in Event Graph#^2fc731|Using event dispatchers]] for the enemy Class to act on is one way of doing things, but this will only work for simple AI. Listed below are ways to control NPCs for a more complex AI.

## 1. AI Control Blueprint
Unreal Engine provides us with a blueprint class just for this, called `AI Control`. Here we can call the `Event On Possess` for controlling the AI. from here, we can call `Cast to <BP Class>`:
![[Pasted image 20240624011959.png]]
And promote as variable. 

Next, in our player class, we set the AI Control option to this AI Control Blueprint:
![[Pasted image 20240624012153.png]]
And create custom events that hooks to our input logic, as shown above (`SimulatePowerLeft` event). Now we can call this event in our AI Control Blueprint, and create our AI logic there! Here's a simple AI for inputting left and right controls with a delay within a random range:
![[Pasted image 20240624012710.png]]


---
Categories: [[020-Game Development]], [[Unreal Engine]], [[Enemy AI]], [[Blueprint Class]]
References:
