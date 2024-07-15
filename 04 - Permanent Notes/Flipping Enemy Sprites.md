---
tags:
---
# Flipping Enemy Sprites
If we're making a 2D-3D hybrid game, becuase both enemies and players can move in all three dimensions, the sprites will rotate in any direction as well. This can be seen if we just let [[Player Aggro|the enemy track us]] without having any additional constraint to movement. While this can make a cool effect, We may want the enemy sprites to move in x-axis only (meaning we will always see the entire sprite). How do we implement this?

Unreal engine provides us with a nifty function called `Find Lookat Rotation` and `Get Forward Vector`. Using outputs from these two, we can set the enemy's `Focal Point` (where it's looking) to x axis only.
![[Pasted image 20240715180048.png]]
From the `Look At Rotation`, we can create a vector from the enemy to the player. We take _only the x element_ of the vector, and set the new `focal point` to `Current Location + Look_at_vector_x`. This way, the sprite will always be "facing" in x_axis direction. By default, the enemy will be looking in its `Forward_vector` direction.

## `SetFocusPoint()` function
Now that we have the basics out of the way, let's actually create the function!

### Step 1. Figuring out when we need to update directions.
First, we need to set when the sprite is eligible for flipping in the first place. It would look weird if the enemy's in its attack animation or stun animation. It'd be even weirder to look for targets (players) if there isn't one. To summarize, we will make the sprites be eligible for flipping only when:
- There is a target (the player instance is valid)
- Enemy is not in its attack animation
- Enemy is not in its stun animation
![[Pasted image 20240715180709.png]]
Using the `AttackTarget` created during our [[Player Aggro]] setup, we can call reference to player character.

### Step 2. Update Focus Point Logic
We need to implement the following logic into our function
```C++
void SetFocusPoint() {
	//--snip
	
	Vector TargetLocation = AttackTarget.GetActorLocation();
	//from possessed event
	Vector SelfLocation = ActionChar.GetActorLocation(); 
	//calculate lookat rotation and
	//create vector
	Vector Lookat = GetForwardVector(FindLookatRotation(Target, Self));

	//get the x axis only and set new focal point
	Vector NewFocalPoint = SelfLocation + Lookat.x;
	Self.SetFocalPoint(NewFocalPoint);

	//--snip
}
```

![[Pasted image 20240715181323.png]]

### Step 3. Get Default Focal Point
The above logic is processed only when conditions in step 1 are met. By default, it will be looking in its `forward vector` direction:
![[Pasted image 20240715181438.png]]
Note that here we're using the `Get ACTOR forward vector`, and NOT `Get Forward Vector`.

### Step 4. Clearing up branch condition

^729e8b

right now the branch condition that decides whether to activate flipping or not looks a bit messy. We can just create a pure function (functions without exec nodes) that returns a Boolean value if the pawn is actionable, like so:
![[Pasted image 20240715182452.png]]
And call this function within our `SetFocusPoint()` function.
![[Pasted image 20240715182529.png]]
This way it's easier to modify when we can act as well.


---
Categories: [[2D Game Dev]], [[Enemy AI]], [[Unreal Engine]]
References:
