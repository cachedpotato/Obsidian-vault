---
tags:
---
# One-Way Platforms
One of the most well-known type of platforms in platformers is the "one-way" platform, where the character can seemingly jump from below, through the platform, and land on top of it. The phrase "one-way" comes from the fact that the player can go through the platform from below to above, but not the other way around. As simple as the concept may seem, it's actually rather complicated to implement.

## The basic idea
Here's how it's basically going to work.
- We know we need to do something in regards to the z axis (up and down)
- We need to somehow detect whether we are above or below this platform.
- If we're below, the collision shouldn't be set to `block`, or else we won't be able to go through
- If we're above, the collision _must be set to block_, so that we can actually stand on top.

To summarize, we need some sort of z-axis detection mechanism that will fire a signal if we're above this platform. Once we get this signal, set the collision of the platform from `overlap` (we can go through) to `block` (we can stand on the platform).
![[Pasted image 20240707213035.png]]

## What we need
Now that we know what we need to do, let's get into details. There are two important things that we need:
- A custom collision type that we can dynamically change
- A Detection mechanism that starts from the feet from our character and goes down a set amount of distance. We will be using a node called `Line Trace For Objects` for this.

## Step by Step Implementation
Now that we have the theory figured out, let's start actually making this thing. First off, the custom collision type.

### Step 1. Custom Collision Type
Under `Edit > Project Settings` we can create custom collision channels under the `Engine > Collision` tab. Click `New Object Channel`, then create new collision channel `OneWayPlatform`.
![[Pasted image 20240707213501.png]]
Next, we need a preset for this channel. Below `Object Channels`, there's the `Preset` settings. Create a new one, and name it the same as our collision channel.
![[Pasted image 20240707213832.png]]
Make sure the `object type` is set to the custom collision channel we've just created.

## Step 2. Creating Platform Blueprint
Create a basic `Actor` blueprint for our platform. We don't need to add any logic here, as it'll be done in our player blueprint. Here we just need to set the sprite, and set the collision option to our own `OneWayPlatform`.
![[Pasted image 20240707213955.png]]

## Step 3. Character Collision Options
![[Pasted image 20240707214233.png]]
Next, we need to set our collision options for our player character. Set the `Capsule Component`'s collision for our player to `custom - Collision Enabled (Query and Physics) - Pawn`. Set the `OneWayPlatform`'s default collision response to `Overlap`. 

## Step 4.1 Setting Scene for Line Trace
Before we use the `Line Trace For Objects` Node, we first need to add a `Scene` component that will be used as the detector and as the starting point of our tracing.
![[Pasted image 20240707214514.png]]
Under capsule component, create a new `Scene` and position it at the bottom of the capsule, where the feet are located.

## Step 4.2 Creating Custom Function and Line Trace Object
We will be creating a function `TraceForPlatform()` that will check for `OneWayPlatforms` every frame. This means this function will be hooked to our `Event Tick` event. Here's the basic logic:
```C++
void TraceForPlatform(self) {
	if (characterMovement.isFalling) {
		if (LineTraceForObjects(
			//start point
			FeetPosition.getWorldLocation(),
			//end point (some distance down from starting point)
			FeetPosition.getWorldLocation() + vectorDown() * checkDistance,
			//what objects to search for
			[OneWayCollision],
			ignoreSelf = True
		) && playerMovement.velocity.z < 0 //falling) {
			setCollisionResponseToChannel(
				CapsuleComponent,
				OneWayCollision,
				Block // We're above - block
			)
		}
		else {

			setCollisionResponseToChannel(
				CapsuleComponent,
				OneWayCollision,
				Overlap //We're not above - overlap
			)
		}
	}
	return;
}
```
Here's the event graph version of the function above (part 1):
![[Pasted image 20240707215453.png]]
Note that the `Is Falling` function really checks for if our character's airborne and not just the falling part. We will get into why we need the extra branch for if we're actually falling soon. 
Here we see the `Line Trace for Objects` in action. We have the start point (`Get world location`) set to the Scene we've created in step 4.1, and some distance down from this scene as end point. We also have the `Object Type` input array, where we define what objects to look for. Here we only need one element - objects with collision type `OneWayPlatform` Setting the `Debug Type` to frame will create a visible line for this trace object, which comes in very handy.
![[Pasted image 20240707215957.png]]
Here's the rest of the function, where we define what to do in case of detection. If we detect something, we will set our `Capsule Component`'s collision response to `OneWayPlatform` to `Block`. If not, we will leave it as `Overlap`.

The reason for having the extra condition for checking if we're falling is because if we immediately set the collision response to block, as we're going up our capsule component will be stuck between the platform, so the game will "launch" our character upwards to sort this issue. To get rid of this launching effect, we need to add this so that when the platform's set to `Block`, the character's completely above the platform.

## Step 5. Fixing Getting Stuck
We are almost done, but we have a small issue. If two `OneWayPlatform`s are close to each other, our character may get stuck between the top platform like the image below:
![[Pasted image 20240707113516.png]]
This happens because the line tracing is still tracing the platform below as we pass the top platform. To fix this, we just need to adjust the distance of our Line Trace's end point. The shorter the distance, the less likely it is for this glitch to happen.

The other glitch is that if the enemy is on top of this platform, it will get permanently stuck unless the [[Wall Detection and Ledge Detection|ledge detector's]] collision option for `OneWayPlatform` (or any other platform in that matter) is set to `block`. Change it to `Overlap` and we're done!


---
Categories: [[2D Game Dev]], [[Collision Detection]], [[020-Game Development]]
References:
