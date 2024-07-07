---
tags:
---
# Player Movement Adjustment in UR
Unreal Engine's default movement options is not optimal for 2D platformers, and feel very floaty. We need to do some fine-tuning to make it feel just right. The following are list of parameters that might need adjustment.

## Gravity
Gravity is the main culprit for "floatiness" that comes with the default options. The default value is set to 1. Higher value means the objects are going to fall harder (I mean it's gravity after all) and lower value means the characters will be more floaty.

## Jump Velocity
Jump Velocity is related to both gravity and jump height. given a constant jump velocity v, if the gravity is higher, the jump height will be shorter. If we want our character to be less floaty but also jump high enough, we need to set both gravity and jump velocity at a higher value.

## Air Control
This controls how much we can move left/right when the player's in the air. Default is set to 0.05, which makes the character barely able to move horizontally if they jump straight up. Setting it to a higher value (~0.3) will make things feel more responsive.

## Use Flat Base for Floor Checks
Because in Unreal Engine, the player hitbox is a capsule, at the ledge the player sprite slightly goes down before falling. to prevent this from happening and make it feel more like a traditional 2D game, we need to set the `Use Flat Base for Floor Checks` option to True.

## Enable Camera Lag
To make the camera slightly go behind the player for a more dynamic look, from `spring arm` check `Enable Camera Lag`. we can adjust how much it lags with `Camera Lag Speed.`
![[Pasted image 20240628185847.png]]

## Constraint To Plane
^a9099f
Unreal engine assumes all games to be in 3d, so the characters will be able to move in all 3 axis direction. This means that whenever a collision happens, there's a chance objects will move in the y axis and fall off our map!
To prevent this, we need to set the `constraint to plane` option in the `character movement` section to true, and increase the `plane constraint normal` value to 1 for the axis we don't want the characters to be moving.
![[Pasted image 20240705183613.png]]
Now our characters will be only moving in x and z axis.



---
Categories: [[Unreal Engine]], [[020-Game Development]]
References:
