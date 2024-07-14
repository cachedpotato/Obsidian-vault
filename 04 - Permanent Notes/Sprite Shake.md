---
tags:
---
# Sprite Shake
To _REALLY_ hammer home the fact that our attack is a meaty one, we can add sprite shakes (just like camera shakes). During [[Hitstun|hit-stun]], we can also make the sprite shake in place a little. This small effect can drastically change the feeling of our attacks. The harder (and longer) the sprite shake, the heavier the attack feels. We can also use shakes to give off some "paralysis" vibes as well.

## Implementing Sprite Shake
Think of a [[Camera Shake Blueprint|camera shake]]. We can have left-right shake, up-down shake, we can adjust the duration and amplitude, etc. While Unreal Engine provides us blueprint class for camera shake, there isn't a built-in function for sprite shakes, so we need to make our own. Luckily, since shakes are just moving sprite positions, all we need are:
- Flip flop to go back and forth between two shake locations
- Timer for the frequency of sprite shake
- Variables for amplitude
- Base location of our sprite (relative)


## Step 1. Get base sprite location
This step is easy. we can just get the values for sprite location at the start (so `Event Start`) with `Get Relative Location` node.
![[Pasted image 20240715010517.png]]

## Step 2. Create `Shake Sprite` Event
This event will later be called in the `ReceiveDamage()` function where we handle our hitstun. To create the effect of a sprite shake, we will be using flip flops. Using the base sprite location we got from step 1, we can alter the location (`Set Location`) of our sprite by adding/substracting some value.
![[Pasted image 20240715011435.png]]
This part is the logic for x-axis shaking (left-right). We can see that both output of the flipflop is connected to `set relative location`. If A, we move the sprite to the left by `Sprite Shake DistX`, and if B, we move to the right. This can be done for all axis, and the idea can be expanded upon, and maybe even add some rotation jittering if we want to go ham.


## Step 3. Call the `Shake Sprite` event in our `ReceiveDamage()` Function
Now that we created the event, we need to call it whenever the hitstun happens. after the hitstun logic, we will be adding a `Set timer by event` node, and call this event.
![[Pasted image 20240715011916.png]]
We want the timer to be looping because we want the sprite shake to Keep shaking and not just stop after one flip-flopping. This value will determine the frequency of our sprite shake.

## Step 4. Ending the sprite shake
The sprite will keep shaking if we just stop it here, so we also need to deactivate this once we're out of hitstun. This can be done using the return value of the `Set timer by event` node, which is a `Handler` for the timer. In the `ClearStun` function, we call `Clear and invalidate timer by handle`:
![[Pasted image 20240715012320.png]]



---
Categories: [[Player Attack]], [[Unreal Engine]], [[020-Game Development]]
References:
