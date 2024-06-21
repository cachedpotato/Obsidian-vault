---
tags:
---
# Creating Wrapper Functions in UR5
Sometimes we want a Blueprint to manage some property of another blueprint. For example, we may want some sprite object to appear only when some game state is reached. While there is a `set visibility` option within the Event graph, it is 'internal', in that it will only take in whatever's defined in that blueprint. 

To solve this, we may want to create a "Wrapper function", like so:
![[Pasted image 20240622000903.png]]
Here, we created a custom function `SetVisibility` (Purple) that executes the `Set Visibility` function UR5 natively provides. Next, we Create a new input field by dragging `New Visibility` from `Set Visibility` to our own `SetVisibility` function.

Within the Game Mode Blueprint, we can create a reference of this object using the `Get Actor of Class` Node. Using this reference, we can call our wrapper function as we see fit:
![[Pasted image 20240622001639.png]]

Using the default `Set Visibility` will not work because that takes `self` as input parameter.

---
Categories: [[Unreal Engine]], [[Blueprint]], [[Useful Nodes in Event Graph]]
References:
