---
tags:
---
# Syncing Blackboard keys with blueprint variables
Having stun state and [[Sprite Shake]] is cool and all, but that won't stop the enemy from following me once in a hitstun. We need a way to halt enemy movement during that period of time. We can do this by setting walk speed to zero, but it may be a bit cleaner to use behavior trees. The plan goes like this:
![[Pasted image 20240715165137.png]]
Following the [[Hitstun]] note, we should have the `IsStunned` Boolean already set, so this should be a breeze...right?
_WRONG_
Behavior trees only interacts with blackboard keys, and we can't automatically sync them with a blueprint variable inside the blackboard nor the behavior tree. What we need is the trusty [[Useful Nodes in Event Graph#^66c2bc|event dispatcher]]. 

## Using Event Dispatcher for syncing
Whenever the `IsStunned` state is changed, we will call the event dispatcher `StunStateChange`. This dispatcher will have a Boolean input value that stores the current `IsStunned` value.

Inside the AI Controller blueprint, under the `Event on Possess`, we can bind the event to the dispatcher, and use the `Change Value as [Type]` Node from blackboard (the same one used for [[Player Aggro]]) to set our Blackboard variable.
![[Pasted image 20240715170514.png]]

![[Pasted image 20240715170535.png]]

## Behavior Tree Branches based on Blackboard key value
Now that the two values (blackboard's `IsStunned` key and our character blueprint's `IsStunned` value) are synced up, we can use the blackboard key inside our behavior tree.

Every Node in the behavior tree has a top part and a bottom part where we can edit. Right clicking the top part gives us options like the following:
![[Pasted image 20240715170811.png]]
From here, select `Add Decorator > Blackboard`, set `Blackboard Key` to `IsStunned` and set the `Key Query` to `Not set` (False). Now this event will trigger only when blackboard's `IsStunned` is false. We will make the enemy `Wait` (Halt completely) if the value is `true`.

We still have one more problem we need to manage. We want the enemy to start moving again once they're out of the stun state. In other words, we need some way to move the enemy from the `Wait` branch to the `Move` branch. This can be done by selecting the `Observer Aborts` to `Both` and `Notify Observer` to `On result change`:
![[Pasted image 20240715171240.png]]
To check if everything's working, pressing `ALT + P` will simulate game in a small window, and show blackboard values on the bottom right.

---
Categories: [[Blackboard in Unreal Engine]], [[Hitstun]], [[Player Aggro]], [[Enemy AI]]
References:
