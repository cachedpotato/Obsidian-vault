---
tags:
---
# The Death-Touch
As much as I _ABSOLUTELY, UNEQUIVOCALLY HATE GETTING HURT ON ENEMY COLLISION_, it is one of the most recognizable enemy "behavior" in games, especially 2D games. You touch the enemy, you die, simple as. I call this the "Death Touch", and despite my grievances with it, it's still very important to know how to implement this in games.

Here's the basic flow of the death touch:
![[Pasted image 20240707001906.png|500]]

## Example Case
In this example, we will be implementing the left route: the player will die if it gets in contact with the enemy.

### Step 1. Collision Settings
First, we need to set our capsule collision settings:
![[Pasted image 20240707002056.png]]
We set the `Collision Response` of `Pawn` from `block` (default), where the player will act as a "wall" that blocks enemy movement, to `overlap`, where the player will overlap and move right past the enemy. We will use the `On Collision Begin Overlap` function to handle what to do next.

### Step 2. Collision Overlap Handling
This example case has a parent class for both player and the enemy, and has function `Defeat` which handles the logic in case of player/enemy defeat. we need to set `On Collision Begin Overlap` event for our player character. What we're doing is simple: just call the `Defeat` function from the parent class on this event.
![[Pasted image 20240707002648.png]]
Make sure the other actor is cast to the enemy blueprint, and to call the `Defeat` function to `self`. We were the one that got hurt after all.

### Step 3. `Defeat()`
This function is 100% our own, so we can do whatever we want with it. Here, we want to launch our player/enemy off screen.
First, we need to set a Boolean variable `IsDefeated`. On `Defeat()`, we will set this to true, and remove collision.
![[Pasted image 20240707003127.png]]
Next, to launch characters off screen, we need to first remove our [[Player Movement Adjustment in UR#^a9099f|planar constraint]] to move in the y (right) direction:
![[Pasted image 20240707003856.png]]
After disabling the plain constraint, we can now `launch` our characters in whichever direction we want! create a custom `LaunchOnDefeat()` function to handle launching:
![[Pasted image 20240707004013.png]]
Connect this with `Set Plane Constraint Enabled` and we have the basis done for `Defeat()`

### Step 4. Adding custom functionality
Remember that the `Defeat()` function is defined in our parent class. This means from setting the `IsDefeated` to true to launching the character is the same for both player and the enemy, but this is not everything that we need to do. For example, for player character, we want to remove controls when we get launched, and also fix the camera at current position as the camera is [[Input System in UR5#^cb5ba8|attached to the spring arm]]. 

To add custom functionality, we need to first call the `Defeat()` function, from the event graph, and also get the parent function call:
![[Pasted image 20240707004835.png]]
After this, we can remove the controls as shown in the image above.
The steps are identical to getting control, except we use `Remove Mapping Context` instead of `Get Mapping Context`.

To detach our camera from the spring arm, we use the `Detach from component`:
![[Pasted image 20240707005056.png]]
The location rule must be set to `Keep World` to make the camera stop at its current absolute position.

We can also add [[Camera Shake Blueprint|camera shakes]] to add more punch to our death animation.
![[Pasted image 20240707011941.png]]


## Step 4.1 Adding Death Animation
With [[PaperZD State Machines]], we can add death animation quite easily. There is one small problem - when do we call the animation? We can get hit by the enemy at any given time - when we're idle, while we're jumping, etc. Do we need to connect `Defeated` state to every other state?

Fret not - PaperZD's creator has already though of this, and provided us with the very useful `Jump` state:
![[Pasted image 20240707012316.png]]
Using jumps we can "bypass" the state machine and jump to the connected animation from our main event graph, using `Get Anim Instance` and `Jump To Node` node:
![[Pasted image 20240707012448.png]]

---
Categories: [[Enemy AI]], [[020-Game Development]]
References:
