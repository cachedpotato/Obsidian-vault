---
tags:
---
# PaperZD State Machines
Consider a movement state machine where we have the following options:
- Idle, when we're not moving
- Walk, when we're moving and on the ground
- Jump (Rise): when we're not on the ground and is rising
- Fall: When we're not on the ground and is falling.

A representation in FSM would look something like this:
![[Pasted image 20240628173407.png|500]]
Now Let's take a look at an implementation of this in PaperZD:
![[Pasted image 20240628173504.png|600]]
_NICE_. 

## Basic Flow
After creating a state machine with `New State Machine` in the `Animation Graph`, double click to get inside the state machine menu. Right click, then choose `Nodes > Animation State` to create a new state. double clicking the state will prompt this menu to pop up:
![[Pasted image 20240628173812.png|500]]
Here we can add the `Play [Animation]` node like the above to choose the animation, and extra logic if needed.

If we have more than 2 nodes, we can connect them if we right click the rim of the state node. This will create an arrow and also the double-arrow sign above. clicking the double arrow sign will prompt yet another menu:
![[Pasted image 20240628174104.png]]
This is where we put in our condition/flags for transitioning from one state to the other. We can move freely between graphs using the sidebar:
![[Pasted image 20240628174303.png]]



---
Categories: [[PaperZD]], [[Finite State Machines]]
References:
