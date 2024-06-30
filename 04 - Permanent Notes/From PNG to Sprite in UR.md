---
tags:
---
# From PNG to Sprite in UR
Once we create (or download) our sprite sheet, we need to convert it to an actual sprite that we can place in UR. The steps are simple:

## 1. Texture Settings
When we first import our sheets to UR, it's extremely blurry. We can fix this by right clicking, selecting "Sprite Actions" then clicking "Apply 2D texture settings". Everything should look a lot crisper (and have proper translucent background!) now.

If it still looks blurry, make sure to double check the filter setting is set to either "default" or "nearest".
![[Pasted image 20240621195825.png|500]]

## 2. Extract Sprites
After applying 2D texture, all that we have left is extracting the sprites. From the same "Sprite Actions" menu, click "extract sprites", and voila, we're done!

### Selecting all textures at once

To expedite the process, we can use the filter function (not the texture, the filter for container) to get every texture at once. Click the filter icon, select "texture > texture". Select all texture files that we want to convert, then do the steps above. This way we don't need to convert them one by one.

## 3. Placing the sprites in the editor
Now that we've successfully converted them into sprites, the only thing we have left is to actually place them. Drag and drop our sprites, and we're done!
...Actually we're not. If we set our background and our player sprite to be in the exact y axis (depth), it will cause mad flickering issues. There are 2 main ways to fix this:

1. Slightly move the player sprite to the forefront, or move the background to the back. Moving by 0.1 should be enough
2. Change the `Material` of our player sprite to `TranslucentUnlitSpriteMaterial`. This way, we don't need to move our character y-axis wise. Make sure that the `show engine content` option is set so that we can actually find and use it.

![[Pasted image 20240621201213.png|600]]
If we can't see the sprite, priority may be the issue. set "Render > Translucent Priority" to 1 (default 0) so that it remains above the background at all times.

## Loading Sprites with functionality
If we load our sprites this way, it wouldn't have any functionality. To make sprites move, trigger animation, etc., we first need to make a [[Blueprint]] of the sprite first. Create a new blueprint with the appropriate, add `PaperSprite` then load our sprite there. Once done, we can drag and drop our blueprint onto the main editor. Make sure to change the `material` and `filter` properties as mentioned above!

## Micro-Adjusting Sprite in real-time
For more advanced games like platformers, we want a more precise way of placing sprites so that it properly touches the ground. To do this, first we need to do a test play. Then, after [[Useful Shortcuts for UR5|gaining control of the mouse]], click the character blueprint instance to get the menu like below.
![[Pasted image 20240628183205.png]]
Here, we can freely zoom in, and adjust position values until we get it just right. Unfortunately, adjusting values here is not permanent, so we need to copy the value and paste it in our character blueprint manually.


---
Categories: [[Unreal Engine]], [[2D Game Dev]]
References:
