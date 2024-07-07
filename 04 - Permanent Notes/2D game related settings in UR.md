---
tags:
---
# 2D game related settings in UR

## Visuals-related 
**motion blur: off**
**anti-alias: select none or fast approximate anti-aliasing**
auto-exposure: off
auto-exposure-bias: 0
dynamic global illumination: lumen > None
reflection method: None
shadow map method: virtual shadow map > shadow map
occlusion options: off (shadowing for 3D)
### Post Processing Volume
Infinite extend unbound: true
EV100: (auto-exposure) - 0
Vignette intensity: 0
Expand gamut: 0
tone curve: 0 (closest to original) 


## Controls related
Refer to [[Player Movement Adjustment in UR]] for more details
`flat based for floor checks`: for more 2D-like ledge detection and falling.

`constrain to plane`: We do not want for the player to move in y axis. setting the value to 1 will completely block the player from moving to that direction.


## Camera related
Spring Arm > Camera
Rotate Spring Arm by -90, absolute rotation

If Camera doesn't need to track player:
- Add Camera in the main editor window
- After getting [[Input System in UR5|IMC]], execute `Get Actor of Class` and select camera
- Hook that and player controller to `Set View Target with Blend`.
- Connect Player Controller to Target, and the camera to `New view target`.
![[Pasted image 20240622013100.png]]
Essentially what we're doing here is mapping our player controller to a new viewpoint from the static camera we created, hence the "Set _View_ with _Target_ with Blend"


## Miscellaneous



---
Categories: [[Unreal Engine]], [[020-Game Development]]
References:
https://ue5study.com/2d/ue5-2d-postprocess-settings/
https://www.youtube.com/watch?v=QVxK2dPJr4g