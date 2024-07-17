---
tags:
---
# Level Transition in Unreal Engine
Unless we are developing a massive, one-map open-world game, we will be moving through multiple maps (or stages). Maps are stored in a separate file, so how do we move from one to the other inside a single game project?
![[Pasted image 20240717112121.png]]

We will create an object that stores a `Name` (or string) of the next map we want to load. Have a hitbox that once overlapped with player, will use the `Open Map by Name` function to load the map.
![[Pasted image 20240717112332.png]]
Here's an example goal object. Have a separate collision box with pawn channel's response set to `Overlap`. Once it overlaps with player character, it will open up the next level.
![[Pasted image 20240717112401.png]]
Here, instead of opening directly, we're sending an event dispatcher that the game mode can receive and process. Why I did it this way I'm...not sure? I just wanted the game mode to handle loading.
![[Pasted image 20240717112624.png]]
Here we can see that the level name we passed in the dispatcher is used to open up next level. Note that we also call a function `StoreVariables`, that will [[Carrying Over variables through Game Instance in Unreal Engine|store player's current data that needs to be transferred over]]. As projects get bigger, we may want to add a [[Loading Screen]] before we load next level.


---
Categories: [[Unreal Engine]], [[Level Design]]
References:
