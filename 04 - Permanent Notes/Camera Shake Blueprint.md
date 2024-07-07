---
tags:
---
# Camera Shake Blueprint
Unreal Engine has a custom blueprint class for camera shakes.
![[Pasted image 20240707010736.png|500]]
For simple camera shakes, choose `DefaultCameraShakeBase`

## Camera Shake Pattern parameters
![[Pasted image 20240707010658.png]]
There are a plethora of parameters to tweak to our own liking. Let's go one by one what it does.

1) Location Amplitude Multiplier: How "Aggressive" the camera shake will be.
2) Location Frequency Multiplier: How frequent the shaking will occur.
3) X, Y, Z: For forward/backward, right/left, up/down shakes, respectively.
4) Rotation Amplitude Multiplier: How "agressive" the rotation shaking will be.
5) Rotation Frequency Multiplier: How frequent the rotational shaking will be.
6) Pitch, Yaw, Roll: For X-axis, Y-Axis, Z-Axis rotational shaking, respectively.
7) Duration: The duration of the shake.
8) Blend in Time: The higher the value, the slower the start of the shake.
9) Blend Out Time: The higher the value, the slower the end of the shake.

## Using the camera shake blueprint
Now that we have the blueprint set up, we need to actually call this to whenever we need camera shakes. To do this, we use the `Play World Camera Shake` node:
![[Pasted image 20240707011436.png]]
Camera shakes are simulated in a "Sphere-like" manner, and we can set the epicenter of this sphere to wherever we want. Here, we set it to player's location using `Get actor location` node. We can see that we called in the Camera Shake blueprint under the `Shake` argument. other arguments include:
- Inner Radius: where the camera shake starts taking effect
- Outer Radius: where the camera shake stops taking effect
- Falloff: dynamic camera shaking - the further away towards the outer radius, the less the intensity of the camera shake

---
Categories: [[020-Game Development]], [[Unreal Engine]], [[Blueprint]] 
References:
