---
tags:
---
# Coyote Time and function overrides
Coyote Time is a brief timeframe when a character is falling off the edge but can still jump (all the while defying laws of gravity). Coyote time is not an adjustable parameter by default, so we need to add it ourselves.

The `Jump` function in UR will trigger only when `Can Jump` function returns `True`. This by default will check if we're on the floor, if we're airborne, etc. To add coyote time, we need to check _on top of this check_ if we're falling of a ledge. This can be done using function overrides.
![[Pasted image 20240707235134.png]]
Under the `Override` option for functions in blueprint, we have the `CanJump` function. Call this, [[Useful Nodes in Event Graph#^1b4fef|Add call to parent]] which is the default `Can Jump` function, then add checks for if we're in coyote time:
![[Pasted image 20240707235337.png]]

As Mentioned before, coyote time activates for a brief moment of time when we're falling off the edge. We need to add a triggerable delay, and after set amount of time, set `IsCoyoteTime` Boolean to false.
![[Pasted image 20240707235604.png]]
Luckily, Unreal Engine has both `Walking on Ledge` event node and `Retriggerable Delay` Node by default, making things a lot easier.



---
Categories: [[Unreal Engine]], [[Player Movement Adjustment in UR]], [[2D Game Dev]]
References:
