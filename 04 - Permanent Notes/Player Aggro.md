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


## Player Aggro Sphere
Now that we know the basics of how aggro works, let's incorporate an "aggro sphere" where the enemy will lock to player only when the player character is inside a certain radius.

From the enemy blueprint, create a `Sphere Collision` and set the radius to however big we want it to be:
![[Pasted image 20240716005804.png]]
Change the collision response setting to `Custom` and set everything to `Ignore` except for `pawn`, which should be set to `overlap`
![[Pasted image 20240716005858.png]]
We know the drill. Create `On Event Begin Overlap` node in event graph, and use the `SetAttackTarget` function we created inside the enemy AI controller blueprint:
![[Pasted image 20240716010005.png]]
We will need `Get AI Controller` node for this as well.
Since we have the aggro set in our enemy blueprint, we can erase the aggro logic we initially set before.


## Additional Stuff with Aggro
The aggro radius will let the enemies _start_ tracking the player, but it will never _stop_ the enemy from tracking. This is because we never implemented a logic for when our player goes out of radius and when enemies should stop targeting the player. This can be done by having a set timer, or just add another event for `end overlap`, or add another sphere to get a range of distance, etc etc. There's a bunch of cool things we can implement regarding Aggro, and the list includes, but is not limited to:
- Aggro Duration
- De-Aggro
- Toggle Aggro
- Stealth
- "Hate" (Commmonly used word for japanese games): for multiple playable characters

---
Categories: [[Enemy AI]], [[Behavior Tree in Unreal Engine]]
References:
