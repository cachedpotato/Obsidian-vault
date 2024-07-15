---
tags:
---
# Player Aggro
One of the most basic Enemy behavior is aggro. If a player is within a certain radius, We may want the enemies to target the player and try to attack. This can easily be done using behavior tree and blackboard.

## Basic player aggro setup
Let's start with a super simple aggro AI. First, in the blackboard, we need to set a new key for the enemies to lock on. Create the `New Key` button at the top left and set the `Base Class` to our player blueprint.
![[Pasted image 20240715160108.png]]

Inside the AI Controller blueprint, we need a function that can dynamically set attack target. Create a function `SetAttackTarget()`, and within the function call `Set Value as Object` using the blackboard reference. 
![[Pasted image 20240715160610.png]]
The `Object Value` should be set as our custom function's input as well. Promote `Key Name` to variable and we must _set it to the same name as the name in the blackboard._ We should also have a new variable that is a reference to our player blueprint object, and set it as the default `Attack Target`.

Back to the main event graph, we need to `Get Player Pawn`, cast it to our player blueprint, then set that as the attack target using the function we just created.
![[Pasted image 20240715160935.png]]

Finally, in the behavior tree, we need to create a new task `Move To`, and set the target to the `AttackTarget` (which should be set to player object) key in our blackboard.
![[Pasted image 20240715161205.png]]

Finally, we need to create a mesh within our map. blueprint instances does not know how to navigate maps by default, so we need to create a new Navigation Mesh. In our main level menu, click `New > Volumes > Nav Mesh Bounds Volume`.
![[Pasted image 20240715161439.png]]
Adjust the size using within the `Brush Settings` option. We can view the actual mesh with by clicking the `show > navigation` option.
![[Pasted image 20240715161623.png]]
If the enemies are within this mesh, they should be able to track player characters now.

---
Categories: [[Enemy AI]], [[Behavior Tree in Unreal Engine]]
References:
