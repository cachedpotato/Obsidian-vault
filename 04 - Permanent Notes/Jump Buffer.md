---
tags:
---
# Jump Buffer
Jump Buffer, along with [[Coyote Time and function Overrides|Coyote time]], are jump-related features that makes our jump/movement a lot more responsive. By default, jumping only works when we _can_ jump, i.e touching the ground (or in coyote time). However, Players more often than not press the jump button _before_ the player hits the ground, so the jumping won't work. While technically speaking it's not really the game's fault, the player won't have a good time if some sort of buffer mechanism does not exist.

## Implementing Jump Buffer
There are multiple ways to add jump buffer, but this method is by far the easiest.
1) Create a boolean value `IsJumpBuffering` and float value `JumpBufferDuration`
2) In the `IA_movement` jump event, add a branch that if `Can Jump` is _false_, we set the `IsJumpBuffering` to True for a `JumpBufferDuration` amount of time. Like coyote time, we will be using triggerable delay. In the _True_ branch we just set it to `Jump()`
3) In the `Event Tick` Node, we will create a branch where if we `Can Jump` _AND_ `IsJumpBuffering`, then we jump.

`IA_Jump`
![[Pasted image 20240708001156.png]]

`Event Tick`
![[Pasted image 20240708001232.png]]


---
Categories: [[020-Game Development]], [[Player Movement Adjustment in UR]]
References:
