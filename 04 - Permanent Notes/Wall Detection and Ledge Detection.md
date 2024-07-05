---
tags:
---
# Wall Detection and Ledge Detection
We see in countless games enemies moving on a platform that seemingly does not just jump off the ledge. Enemies also seem to know when there is a wall and turn around once it reaches one. How do we implement this?

## Wall Detection
Wall detection is the easier of the two so let's start with this one first.
![[Pasted image 20240705234056.png]]
We will add a collision box in front of the enemy sprite, and call a function that rotates the enemy when this collision box hits the wall.
![[Pasted image 20240705234257.png]]
First things first, let's make the enemy (pig in this case) move forward by default. this can be done by using the `Get Actor Forward Vector` function and connecting it to `add movement input` in our Enemy [[Controlling Enemy AI | AI Controller Blueprint]].

Next, we add a `Box collision` as a child of our capsule component and set it in front of the enemy sprite:
![[Pasted image 20240705234544.png]]

We Then call the `On Component Begin Overlap` function on our event graph, and create custom function `Rotate Char`, which goes something like this:
```C++
BoxCollision WallDetector;
if (WallDetector.OnComponentBeginOverlap) {
	SetActorRotation(
		self,
		CombineRotators(GetActorRotation, (0, 0, 180))
	);
}
```
In Blueprint it looks like this:
![[Pasted image 20240705235049.png]]

Now our enemy will detect walls!

## Ledge Detection
Unlike Wall detection, ledge detection needs to be done constantly, that is, it needs to check if it's at the ledge every frame. This means that we need to use a different function, and use the `Event Tick` Event.
![[Pasted image 20240705235454.png]]
Similar to Wall detection, we will add yet another `Box Collision` component. However we will set it a little bit more towards the front and a bit downwards. The reason for using `Event Tick` becomes more clear - we need to check the length of the collision between the floor and this collision box all the time. Once the length hits 0, we can safely assume we're at the ledge.
![[Pasted image 20240705235708.png|500]]
After adding the box collision component, we need to create a custom function `CheckLedge`:
![[Pasted image 20240705235822.png]]
Here we do not use the `On Compoenent Begin Overlap`. Instead, we `Get Overlapping Actors`, and get the `length` element. If this becomes 0, then we're at the ledge, so call the `Rotate Char` function we made earlier.

This will work, with one small problem: The enemy will rotate when it's in the air as well, as the length of collision is also 0 there. This means before we execute this logic, we first need to check if we're on the ground:
![[Pasted image 20240706000137.png]]
After dragging the `character movement` asset, we use the `get current floor` node and check if current floor is a `walkable floor`. If not, we won't execute the logic.

---
Categories: [[Enemy AI]], [[020-Game Development]]
References:
