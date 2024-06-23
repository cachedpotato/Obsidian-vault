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



## `Destroy Actor`
Destroys `self`. 

## `Cast To <Actor>`
Checks if the cast is compatible to the `<actor>`. In other words, checks if whatever's activating this node can be changed into `<actor>`. has three output branch:
- `exec`: for next part of the logic.
- `Cast Failed`: executed upon failure
- `As <Actor>`: sets command for the `Actor` that triggered this event.
ex) `As BP_ThirdPersonCharacter > Jump > Target`: after this event is triggered, the `ThirdPersonCharacter` instance will `jump`. 

Cast is extremely versatile but also quite heavy. Use `interface` instead for heavier logic.

## Get/Set Relative Location
Self explanatory. Get/sets the relative location. We can store this as a variable then pass it to something else.

## Timeline
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

## Is Player Controlled
Checks if the object is controlled by a player (possessed), and returns a Boolean Value. Useful for functions that changes behavior depending on whether if it's triggered by a player or an NPC

## Event Dispatcher
From my understanding, event dispatchers is a "message passing" event that signals certain event has triggered, hence the envelope logo at the top right corner:
![[Pasted image 20240622125022.png]]
This is useful for controlling enemy AI. Since we don't input the controls ourselves, we let the NPC get a dispatcher, and upon receiving the info, call some other event/function to process. Here's an example:
![[Pasted image 20240622125308.png]]
The `DrawPhaseStarted` Event Dispatcher is defined in the Game mode blueprint. Once we receive the dispatch, we can create a custom event or connect a pre-existing event. The naming convention for this is `On{EventDispatcherName}`. Here we can see that the NPC will `Attack` after a `AttackDelay` amount of time.

---
Categories: [[Unreal Engine]]
References:
https://www.youtube.com/watch?v=4D5UfHZx_qU
