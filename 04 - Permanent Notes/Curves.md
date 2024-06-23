---
tags:
---
# Curves
Curve is an Unreal Engine asset that lets you create curves. Just like in [[Useful Nodes in Event Graph#^084440|timelines]], we can freely create keyframes and create curvatures. We can then use this as a variable to change multiplier/variable values or any other situations where curves might be useful.

Curves come in 3 types:
- curve float
- curve linear color
- curve vector

Below is an example usage of curve float.

## Example: Using curves as multiplier
Consider a game where we mash buttons to increase speed of the our player character (runner). The harder we mash, the faster the runner becomes. The simplest way of doing things is to increase speed by adding a constant value to current speed (`maximum walk speed` in UR):
![[Pasted image 20240623174655.png]]
This definitely works, but because the speed increases in a constant rate, it's rather unnatural. The faster the runner is currently running, the harder it will be to gain more speed. To add this sense of "realism" to our game, we may want to use a multiplier to our speed increase constant `SpeedIncreasePerTap`, where the multiplier is a function that takes the current speed as input and returns a value between 0 and 1:
```c++
currentSpeed += multiplier_curve(spedIncreasePerTap);
```
We can do exactly that with the curve asset!
First, create a new `curve` asset by right clicking > `miscellaneous` > `curve`. 
Then, we add key frames where we want them to be. For this case, the maximum possible speed is 1500, and the lowest 0. When the speed is low, we want the multiplier to be near 1, because it's easer to gain speed at the start. If we're near max speed however, gaining speed will be a lot harder, so we want the multiplier to be around 0.1. 
Add these two key frames ((0, 1) and (1500, 0.1)), right click then set to auto. This will automatically create a smooth curve that connects the key frames, and a knob we can use to change the curvature with:
![[Pasted image 20240623175519.png]]
Now all we need to do is to import this to our player blueprint. Under Variables, add a new `Curve Float`, drag it onto the event graph, then connect it to `Get Float value`. The target should be the curve we created, and the `In Time` should be connected to the `x` value, which in this case is the speed (or length of speed vector):
![[Pasted image 20240623175927.png]]
We've successfully created our custom multiplier function and hooked it to our base speed increase rate!


---
Categories: [[020-Game Development]], [[Unreal Engine]]
References:
