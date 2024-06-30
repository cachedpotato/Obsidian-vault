---
tags:
---
# Basic 2D Input in Unreal Engine
There's a bit more to left-right movement than just adding IMC and Input actions into the blueprint. This is a comprehensive summary of how to get the input/controls started for 2D platformers.

## Step 1. Input Actions and IMC
Nothing too special for jump, but for left/right movement we need to change the `value type`. For the former we need to select `Axis1D(float)` because we will be moving in a line (jump is separate).

For the input mapping context, after adding the `jump` and `move` actions we need to do two things for `move`:
1) set left _AND_ right control inputs
2) set the left modifier to `negate` (we're going the opposite direction)
![[Pasted image 20240628152013.png]]

## Step 2. Adding Controls to player
Nothing special here. Add spring arm and camera, in the event graph add player controller and IMC, and add `jump` and `move` input actions into the graph.

## Step 3. Jump
Unreal Engine already has a built-in node for jumping: `jump` and `stop jumping`. Connect these two to input actions.
![[Pasted image 20240628152244.png|500]]

## Step 4. Move
First, we need to connect `Add Movement Input` to our `IA_move` event:
![[Pasted image 20240628152339.png|500]]

This will make our character move, but there are two problems:
- The camera flips with us when we go left
- The sprite does not flip when we go left

### 4-1. Camera setting
All we need to do for the camera to stop moving with us is to set the spring arm's rotation to "absolute(world)" and not relative:
![[Pasted image 20240628152735.png]]

### 4-2. Flipping the movement animation
Contrary to what we think we need to do, which is rotating the sprite based on movement vector, what we actually need to do is rotate the _controller_. Easiest way to do this is to create a function `UpdateControllerRotation` and check if we're moving left every tick. The function will:
- get the velocity of x
- compare with 0 and see if we're going left
- If true, set controller's z rotation (yaw) to 180
![[Pasted image 20240628153155.png]]
Here we're using a `rotator` for more modularity.

The bare bones are now done! We still have some [[Player Movement Adjustment in UR|fine-tuning]] for smoother control but this will get things going just fine.


---
Categories: [[2D Game Dev]], [[Unreal Engine]], [[Input System in UR5]]
References:
