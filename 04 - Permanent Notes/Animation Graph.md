---
tags:
---
# Animation Graph
Animation Graph is at the heart of `PaperZD` Plugin. This Note will briefly summarize what functionality it has.

## Output Animation
This is the output function of the animation. It will play whatever animation is being passed in. We can hook an animation directly to play that animation without any conditions (so basically play that all the time), or we can add conditionals, or even state machine.

## Play `[AnimationName]`
The animation name is decided in the Animation Source asset.

## Select Animation by `[Method]`
The main function for selecting animation.  There are many ways to select animation, the simplest of which is by Bool:
![[Pasted image 20240628164040.png]]
Here we're using the movement vector of our character as the conditional. If vector is 0 (not moving), then we play the idle animation. if bigger than 0, we play the running animation.

If we use the PaperZD plugin just like this, we're not really using it to its full potential. This is nothing too different from regular sprite selection procedure after all. What we can use instead, is State machines.

## State Machine
In addition to all the animation related function described above, PaperZD also gives us the ability to create state machines:
![[Pasted image 20240628164701.png|500]]
The best part about this is that it's extremely easy to manage, compared to normal methods where we'd have to add a bunch of branches and selection nodes. Details can be found [[PaperZD State Machines|here]]. 




---
Categories: [[PaperZD]], [[Unreal Engine]], [[2D Game Dev]]
References:
