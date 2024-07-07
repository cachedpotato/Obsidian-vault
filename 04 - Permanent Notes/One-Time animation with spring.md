---
tags:
---
# Springs
Springs in Games will launch player to heights unreachable by jump alone. Implementing springs are quite simple:
- Add Collision Box at the top of the spring platform
- On collision overlap, launch player
- Play spring animation
- Go back to idle

While I did say it's simple, it's good to know how to play an animation just once. Here's how to do it.

## One-Time Animation Steps
1) Set Looping of flipbook to false
By default the spring's idle animation will be on loop (which is basically one frame over and over again). Set this looping animation to false.
2) [[Useful Nodes in Event Graph#^d18170|set flipbook]] animation to activated Animation
3) Play the animation
4) When the animation ends (`On Finished Playing`), return to idle
Flipbook has custom event called `On finished playing`. Because we turned the looping off, we need to set this back on again, and set the flipbook back to idle flipbook once it ends. We will be using `On Finished Playing` Event for this.

![[Pasted image 20240707224353.png]]
![[Pasted image 20240707224415.png]]
![[Pasted image 20240707224427.png]]

---
Categories: [[Collision Detection]], [[Unreal Engine]]
References:
