---
tags:
  - NeedWork
---
# Attack Animation and Animation Overrides
Attack buttons can be used in any situation - while we're walking, at idle, jumping, etc. While we can add some constraints to attack, from a developer standpoint we should minimize such constraints. For example, while we can make our players not move when we're in an attack animation, or disallow [[Attack Cancelling]], we shouldn't straight out deactivate the attack input while the player character's moving. 
To achieve this in PaperZD, [[The Death-Touch#^883e5c|utilizing jumps]] may be one way of doing things, but there's an easier method for this - animation overrides. Animation override does what it exactly says in the name - it will override the current animation with a new one. using this in tandem with an `IsAttacking` Boolean value like we did with [[Coyote Time and function Overrides|coyote time]] we can freely modulate our attack motion behavior.

## Animation Override
To use animation override, we need to create a slot for it first:
![[Pasted image 20240714162455.png]]
From the Animation Blueprint, create a new node `Override Slot` out of the State machine. Next, in our player blueprint, we first `Get Anim Instance` and connect that to `Play Animation Override with Callbacks`. Make sure the slot name matches with the one we created above!
![[Pasted image 20240714162427.png]]
Set the animation sequence to the one that we need (in this case the attack animation) and we're set. The `IsAttacking` Boolean is there to disable attack cancelling, as without it the character will start the attack animation _whenever the attack button is pressed_. Sometimes we want that do happen, but by default we should have the attack animation play at its entirety so that the players aren't able to just mash their way to victory.

## Adding Modularity
Just by adding a Boolean value `IsAttacking`, we can restrict/enable attacks at various situations. Here are a few examples.
1) Movement
If we don't want the player to be able to move when we attack, We can do that by simply adding a branch that goes:
```c++
void IA_Move(bool isAttacking, std::vector<int> movement) {
	if (!isAttacking) {
		add_movement_input(movement[0], movement[1])
		//movement related
	}
	return;
}
```

![[Pasted image 20240714163308.png]]

The same can be done with jumps:
![[Pasted image 20240714163407.png]]

2) Attack Cancel
Our default option for attacking disables attack cancelling, by allowing the attack animation to be initiated only when `isAttacking` is false. Getting rid of this branch will enable attack cancelling altogether. We can possibly incorporate delays to allow attack cancelling after a certain period of time as well.


## Adding More Attack Options





---
Categories: [[PaperZD]], [[Player Attack]], [[020-Game Development]]
References:
