---
tags:
  - MaySplit
---
# Projectile Throw Animation and Sockets
Unlike other animations that are bound to character sprites, projectile throws are special in that there are two distinct animations playing at once:
- From player: the throwing animation
- From projectile: projectile animation (think of fire animation for hadouken)

We also need some way of positioning projectiles so that it doesn't just spawn inside our player sprite, and just like attack animations we want it to spawn at a certain frame of the animation rather than just the beginning. While using trial and error for positioning and [[Adding Sound Effects in UR|using the `get playback position`]] will work, we can make the process cleaner with PaperZD's Notifies and Sockets.

## Sockets in Unreal Engine
Sockets in and of itself are just, well, sockets, that we can place objects onto. In fact, one of the most common uses of sockets is placing hats onto character models. However, we can also use it to get precise location that we can use for spawning various objects.

For throw animations, we can create a socket `SwordThrow`, and place it where the sword will spawn. Select the _sprite of the frame we want the sword to be spawned_, and create a new socket item in the socket array.
![[Pasted image 20240716181637.png]]
There's some jank with sockets, though. because the default animation for player character is the `idle` flipbook, we need to set it in one of the frames in the idle animation as well. luckily, we just need to get the name of the socket we made here, and not the position.
![[Pasted image 20240716181900.png]]

Now that we have the socket set up, we can create a scene (that we'll use the location of as the spawn location), and set the `Parent Socket` to the socket we created. 
![[Pasted image 20240716182228.png]]
Below shows how we can use the scene component's location for spawn position
![[Pasted image 20240716182131.png]]

## Process function in a certain frame using Animation Blueprint
So far we have:
- Set the throw animation
- Set spawn position of the projectile
Now we need to set _When_ the project will be spawned. This can be done using PaperZD's Notifies.
Inside the Animation source folder, we create a `new notify` at the frame we want the sword to be spawned:
![[Pasted image 20240716182637.png]]
Clicking the `Animation Blueprint` button on the top right will open the animation blueprint folder, where we can find out that a new function has been created:
![[Pasted image 20240716182754.png]]
This is a function that is called when the notify is received. Here' we just get the player reference and call the throwing event:
![[Pasted image 20240716182843.png]]

---
Categories: [[Projectiles in Unreal Engine]], [[Attack Animation and Animation Overrides]], [[PaperZD]], [[Unreal Engine]]
References:
