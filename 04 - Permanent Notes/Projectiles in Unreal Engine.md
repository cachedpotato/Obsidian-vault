---
tags:
---
# Projectiles in Unreal Engine
Having player have a projectile attack can add some variety than just "mash same button to attack". However, to incorporate projectiles, we need to figure out how to
- Create a projectile
- Create Hitbox and collision responses
- Spawn projectile from player
etc. etc.
While we won't cover everything here, we will be going through the basics.

## Step 1. Creating Projectile
First we need to create a separate blueprint for our projectile to set hitbox/flipbooks. For simple projectiles, a basic `Actor` blueprint should suffice.
Once we have the flipbooks and hitboxes set up, there are two things we need to do.
### Setting the New Box Collision as root
By default the hierarchy of components is:
```
self (root)
	Default Scene
		Box Collision <- we just created this
...
```
We want the Box collision to be the root for the next step to work. All we need to do is to drag the `Box collision` up to where `DefaultScene`. This will change the Hierarchy to:
```
Self(root)
	Box Collision
```

### Adding `ProjectileMovement` Component
Unreal Engine provides us with a handy `Projectile Movement` component that we can use to adjust various projectile related settings. One of the more important options are the `speed` settings:
![[Pasted image 20240716154622.png]]
This determines how fast the projectile will move. Of course we can later dynamically change the speed using [[Useful Nodes in Event Graph#^1e3a9e|timeline]]. 

### Can player Jump on Top?
There are projectiles that doesn't just serve as an attacking tool, but also as a platform. Surely there is not a setting native to unreal engine that -
_Yes, there is._ Under the `Collision > Can Character Step-up-on` setting for `Box Collision` (or any collision-related component). In fact, the default is set to true!
![[Pasted image 20240716154953.png]]

## Step 2. Collision Settings
While this is not really something that's specific to projectiles, it's good to go through what we may want to consider.
![[Pasted image 20240716160254.png|500]]
### Environements
Often prefixed with `World`, these collision channels usually deal with the environment, such as the floor, ceiling, wall, etc. If we want our projectiles to stick to the wall, we want those channels to be set to `Block`.
### Pawns
For players and enemies, we may want them to inflict damage, then disappear. Generally Speaking, if the collision box needs to interact with something in some way, the default should be `Overlap` and not `Block`, and `Ignore` channels that the collision box should not interact with.
### Events
`OnEventBeginOverlap` is used for collisions interacting with channels that are set to `Overlap`. For _solid_ objects, like floors or walls, we want to use `OnEventHit`.

## Step 3. Stuck Animation
The default animation for projectiles will most likely be the one used during the actual "Firing" phase of the projectile. If we have different flipbooks for when it gets stuck in something, we need to change the flipbook. While we CAN use [[PaperZD]], for cases as simple as this we can just use the default method of calling `Set Flipbook` and `Set Looping`.
![[Pasted image 20240716160746.png]]
If the flipbook is offset, we can always create a scene under the hitbox component and make the flipbook's relative location move to there. For players to actually step on the hitbox, we need to change the pawn channel's collision response (currently set to `Overlap`) to `Block`, and have the `Can Character step up on` set to `true`.
![[Pasted image 20240716160952.png]]

## Step 4. Inflicting Damage
For this part, we will be using the `EventBeginOverlap`. Cast the `other actor` to our enemy blueprint, and call function for inflicting damage, along with other stuff we want the projectile to do. To remove the projectile afterwards, call the `Remove Actor` node.
![[Pasted image 20240716161213.png]]

## Step 5. Throwing the Projectile
The projectile side of the setup is now complete. Now we need the player character to be able to actually throw the thing. To do this, we need a `Spawn Actor of Class` Node. 
![[Pasted image 20240716161516.png]]
The node contains some important parameters:
- `Class`: the actor class to spawn. Call the projectile blueprint.
- `Spawn Transformation`: can be split into
	- Spawn Transform Location
	- Spawn Transform Rotation
	- Spawn Transform Scale
- `Collision Handling Override`: For collision interaction in the event of spawning in. By default, if the projectile is spawned in a location deemed not "spawnable", it wont. by changing it to `Always Spawn, Ignore Collisions`, we can spawn it whenever it is called.

The return value is set as a reference to the spawned object which we can store and use. For example, we may want to remove the previously thrown projectile once a new one is thrown. To do this, we need a reference to the spawned projectile object. Check its validity (if there's no projectile, the reference will not be valid), and if it is, remove the referenced projectile first before spawning a new one.
![[Pasted image 20240716162133.png]]
We can use the `Sequence` node for the ordering of events. While this will work if we want to keep just one projectiles, if we want to keep more than one, we may want to create an array that stores the projectile references. if the array size becomes bigger than our set size, then we remove the oldest projectile.
![[Pasted image 20240716164541.png]]

[[Projectile Throw Animation and Sockets]]


---
Categories: [[Player Attack]], [[Collision Detection]], [[020-Game Development]]
References:
