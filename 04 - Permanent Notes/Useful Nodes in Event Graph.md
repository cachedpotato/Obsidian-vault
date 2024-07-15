---
tags:
---
# Useful Nodes in Event Graph
## Branch
Acts as the `if` statement in programming language. Takes condition and input, and provides two branches, one for if the conditions are met and the other for when they're not.

## Switch
Makes something activate only when some condition is met. Similar to branch in that it takes some input that will serve as a "condition", but still serves a different purpose as switches completely stops the logic from proceeding when the conditions aren't met. This is especially useful for `Event Tick` as this by default is processed every frame.

We can also use it as `match` with enum values as well.

## Select
If we have a switch/branch that connects to the same function, instead of copy pasting the function to each of the arms it can be a lot cleaner to just use the select node instead.
![[Pasted image 20240622085835.png]]


## Flip Flop
Will alternate between two inputs. Inputs can be events as well.

## Clamp
Sets the min/max possible value of a variable

## Get/Set Relative Location
Self explanatory. Get/sets the relative location. We can store this as a variable then pass it to something else.

## Get Flipbook

^d18170

Useful for changing flipbook based on a certain condition. For example, we may want to dynamically change the running animation's play rate depending on the current length of the velocity, but not necessarily for idle animation. We can do logic akin to:
```c++
void setPlayRate(player) {
	if (player.sprite) == "running" {
		player.sprite.playrate = movement.velocity.length()/movement.maximumVelocity;
	} else {
		player.sprite.playrate = 1;
	}
}
```
to do this in event graph, we need some sort of way to grab the current sprite and check if its the 'running' flipbook or the 'idle' flipbook. This is where the `get flipbook` node comes in handy:
![[Pasted image 20240623171120.png]]

## Timeline
^084440
Timeline node allows values to be keyframed over time. There are three outputs:
- Update
- Finished
- Direction\
Update is triggered _every frame_.

### Tracks in Timeline
By double clicking the timeline, we get into a special page for tracks. Here, we can add tracks for variables or values we want to change over time:
![[Pasted image 20240621222036.png]]
Looks pretty similar to what we do in FL studio or any other DAW in that matter, actually.
Like DAWs, we can also create multiple key frames, then create a smooth curve out of those lines by selecting all key frames that we want and right clicking:
![[Pasted image 20240621223440.png|600]]
The true beauty of timeline is that we can actually pass _Events_ as track inputs. When creating a track, we are given these options:
- Float
- Vector
- Color
- Event
Depending on the event track, the significance of the value we set for our key frame may vary, but we can do things like this:
![[Pasted image 20240622114547.png|500]]
Here we passed a function `Set Sprite`, where we switch to a new sprite. This is connected to an event track in the timeline, which has a keyframe at some time $t$. This means that after $t$ much time has passed, this function will trigger and change sprite.

Oh right, if the timeline is for some action that's going to be repeated over and over, _MAKE SURE THAT IT'S CONNECTED TO PLAY FROM START_, or else it'll automatically save the last state it was in and immediately start from there rather than the beginning.

## Lerp
^a8fe06
Lerp stands for "Linear Interpolation". We input A, B and Alpha, which serves as a parameter that acts as the mediator. To reuse the image I made before:
![[Pasted image 20240621221359.png|450]]
Here, the `t` serves the same purpose as alpha in lerp. 


## Get Actor of Class
This is a rather heavy operation, so It's not recommended to hook this to something like `Event Tick`. This is used for creating a reference of something that is outside of the current blueprint. For example, if we want some value within BP 1 to control a function in BP 2, we can use this node, set the `Actor Class` to the function we want to reference, and promote the output to a variable, like so:
![[Pasted image 20240621235012.png]]

## `Destroy Actor`
Destroys `self`. 

## `Cast To <Actor>`
Checks if the cast is compatible to the `<actor>`. In other words, checks if whatever's activating this node can be changed into `<actor>`. has three output branch:
- `exec`: for next part of the logic.
- `Cast Failed`: executed upon failure
- `As <Actor>`: sets command for the `Actor` that triggered this event.
ex) `As BP_ThirdPersonCharacter > Jump > Target`: after this event is triggered, the `ThirdPersonCharacter` instance will `jump`. 

Cast is extremely versatile but also quite heavy. Use `interface` instead for heavier logic. `Cast to Actor` is often used for getting game modes into player blueprints.
## Is Player Controlled
Checks if the object is controlled by a player (possessed), and returns a Boolean Value. Useful for functions that changes behavior depending on whether if it's triggered by a player or an NPC

## Is Moving on Ground
Checks if the character/object is on ground or not. Useful for jump animations

## Event Dispatcher

^66c2bc

^2fc731
From my understanding, event dispatchers is a "message passing" event that signals certain event has triggered, hence the envelope logo at the top right corner:
![[Pasted image 20240622125022.png]]
This is useful for controlling enemy AI. Since we don't input the controls ourselves, we let the NPC get a dispatcher, and upon receiving the info, call some other event/function to process. Here's an example:
![[Pasted image 20240622125308.png]]
The `DrawPhaseStarted` Event Dispatcher is defined in the Game mode blueprint. Once we receive the dispatch, we can create a custom event or connect a pre-existing event. The naming convention for this is `On{EventDispatcherName}`. Here we can see that the NPC will `Attack` after a `AttackDelay` amount of time.

## Set Timer by Event
In the main event graph, we can just use `delay` for creating delays. For functions however, this is not available. Instead, we have to use the `Set Timer by Event` node:
![[Pasted image 20240624010513.png]]
To activate an event after a set delay, we have to get a `create event` node from the `Event` out from `Set timer by event`, and call our event there. The `time` is where you input your desired delay time. This can be used for enemy AI controls or [[Resetting the Game]]

## Add Call to Parent Function
^1b4fef
This will be used for all child instances where we want to do some extra, child-exclusive logic not present in parent's function. 
![[Pasted image 20240707000521.png]]


## Launch Character
Used to launch characters in set direction.

## Play Sound
There's two options for playing sound:
- Play Sound at Location
- Play Sound 2D
The first option will give a more "roomy" feel whereas the latter will give us a flat sound.

## Set Collision Response To Channel
Used to update collision response depending on collision channel, as can be seen through the example of [[One-Way Platforms]].

---
Categories: [[Unreal Engine]], [[Enemy AI]]
References:
https://www.youtube.com/watch?v=4D5UfHZx_qU
