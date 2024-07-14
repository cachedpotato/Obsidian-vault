---
tags:
---
# Hitstop
To add a bit more of a punch to our attacks, we may want to incorporate what's called a hitstop. If the [[Hitstun]] is for the "receiving end" of the attack, hitstop goes both ways - it temporarily "freezes" player and the enemy for a brief period.

## Implementing Hitstop
All we need to do is to create a custom event `HitStopSequence` and use the node `Set custom time dilation`. If this value is set to 0, the actor freezes in place and movement is disabled. Default value is 1.
![[Pasted image 20240715005447.png]]
We use the `Retriggerable Delay` Node so that we hitstop delay happens whenever the hitbox collision overlap is triggered. Just call this custom event on both the target and self whenever the overlap event happens, and we're all set!
![[Pasted image 20240715005642.png]]

---
Categories: [[Player Attack]],
References:
