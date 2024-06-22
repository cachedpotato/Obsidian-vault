---
tags:
---
# Moving Relative Position in UR
In games where most things are static, Moving sprites may not be determined by traditional directional input. We still may want to move sprites around, and to do that we need to Get/Set relative positions.

First, we need to set where we want to move. While we can just wing it and test values, it's better to have a more concrete look. Luckily, we can use Scenes for this.
## Step 1. Creating Scene Instance

In Viewport, we can create a scene instance, the position of which we can use as the end point of the movement. If we first create a scene instance, however, nothing's there and it's quite hard to see where it's located. We can alleviate this problem by adding a `billboard`:
![[Pasted image 20240622113316.png]]
Cool thing about billboard is that this is just a placeholder, and will not appear in actual gameplay.

## Step 2. Getting the Relative Position

In the blueprint event graph, drag in the sprite you want to move around. We can simply get the relative position by connecting this with the `Get Relative Position` node.
![[Pasted image 20240622113002.png]]
We can then make this as a variable, which we can use for actual movement.

## Step 3. Creating Movement with Timeline
As discussed [[Useful Nodes in Event Graph#^a8fe06|here]], we can use Lerp and Timeline to move from Point A to Point B, and create more flair by tweaking the alpha value. Here's how it looks like in the event graph:
![[Pasted image 20240622113930.png]]
We're setting our new relative position with Lerp, which we pass our initial position `Default Position` and the end point position from the `AttackPos` which is the scene instance we created. The alpha value is changed using `Timeline`, and the play rate of this can be changed using the `Set Play Rate` Node (at the far left).

---
Categories: [[2D Game Dev]], [[Unreal Engine]]
References:
