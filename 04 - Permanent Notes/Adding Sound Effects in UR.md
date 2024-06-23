---
tags:
---
# Adding Sound Effects in UR
If we break down the process of adding sound effects, it comes down to these 3 core steps:
- Get the frames in which we should play the sound
- Make sure we play in that frame ONCE
- Actually get the sound and play.

The reason why second step exists is because a single frame can process multiple ticks, depending on the CPU/GPU.

## Step 0. Getting the sound
Nothing special, except for cases where we have multiple sound bytes for a single action, for example footsteps. In these cases, we create what's called a "sound cue":
![[Pasted image 20240623185112.png]]
Here we've created a footstep cue with 2 sound bytes. By default, Sound cues will pick one of the sounds at random, but we can always adjust the settings.

## Step 1. Get the frames
Look through the flipbook and find the exact frame when each foot land on the ground. Let's say they're 1 and 5. We want our sound effect to play at those frames, so in the event graph we use `Get Playback Position In Frames`:
![[Pasted image 20240623185318.png]]
This is essentially the `if` part of: 
``` c++
if (sprite.PlayBackPositionInFrames == 1 || sprite.PlayBackPositionInFrames == 5) {
	DoOnce(play_sound(sound));
}
```

## Step 2. Do Once
As Mentioned above, we need to make sure the sound effect is played only once. To do that, we use the `Do Once` node:
![[Pasted image 20240623185609.png]]
Here we set the sound to play once and only once when the conditions (frames 1 and 5) are met. If not, we "reset" this, and start over. For example, in frame 1, we go in the `true` branch and play the sound. on frame 2, we get the `false` Boolean value, so this resets.

## Step 3. Play the sound
Use either the `Play Sound 2D` or `Play Sound at Location` for actually playing the sound. Make sure to select the sound cue we've created in the `sound` option! There are also volume/pitch multipliers and other good stuff that we can control, but that's not the focus of this note.

---
Categories: [[Unreal Engine]], [[Useful Nodes in Event Graph]] 
References:
