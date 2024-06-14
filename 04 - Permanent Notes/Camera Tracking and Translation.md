---
tags:
---
# Camera Tracking and Translation
Besides clamping or collision detection, there is scrolling - or in a different perspective, the movement of the camera - we need to think about when it comes to player movement. We almost always want our player character to be visible, preferably near the center point, so that most of our attention goes there. So how do we add camera behavior for tracking player?

## Translate
translation is the term for shifting the x and y coordinate system. Using translate, practically we're not really moving the _camera_ around. Rather, we're moving the _very level itself_. let's take a look at the low-level code.

```lua
local CHARACTER_MOVE_SPEED = 200
function love.update(dt)
	if love.keyboard.isDown('left') then
		characterX = characterX - CHARACTER_MOVE_SPEED * dt
	else if love.keyboard.isDown('right') then
		characterX = characterX + CHARACTER_MOVE_SPEED * dt
	end
end 

cameraScroll = characterX - (VIRTUAL_WIDTH / 2) + (CHARACTER_WIDTH / 2)

function love.draw()
	push:start()
		love.graphics.translate(-math.floor(cameraScroll), 0)
		--snip
		love.graphics.draw(characterSheet, characterQuads[1],
			 math.floor[characterX], math.floor[characterY]) 
	push:finish()
end
```
first, we define the character's X position with `characterX`. then we define variable `cameraScroll`, which ensures that the character is always located at the center. 
![[Pasted image 20240614170545.png]]
Kind of hard to see (despite me spending 20 minutes on this), but the brown square is the translated screen. We can see that the character, originally at the right, is now at the center again. Wait, you say, we added `-cameraScroll`, how come you did the opposite in the picture? Well I didn't, I just did not have any screen real estate. The brown display will show the image that's moved to the LEFT, not the right, the arrow just shows the position where the character will be located.


---
Categories: [[Game Development]], [[CS50 - Game]]
References:
