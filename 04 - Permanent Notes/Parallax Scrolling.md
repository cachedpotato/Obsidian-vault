---
tags:
---
# Parallax Scrolling
We all know what parallax is - stuff at the background moves slower than the stuff at the foreground. By having two different "planes" move in different speeds, we can create a feeling of depth into a 2D game.

How do we actually implement this in code? for 2D games, we can set variables for foreground scrolling speed and background scrolling speed separately.
```lua
local backgroundScroll = 0
local groundScroll = 0
local BACKGROUND_SCROLL_SPEED = 30 --slower
local GROUND_SCROLL_SPEED = 60 --faster

local BACKGROUND_LOOPING_POINT = 413

function love.update(dt)
	--scrolling logic
	backgroundScroll = (backgroundScroll + BACKGROUND_SCROLL_SPEED * dt)
		% BACKGROUND_LOOPING_POINT

	grondScroll = (grounScroll + GROUND_SCROLL_SPEED * dt)
		% VIRTUAL_WIDTH
end

function love.draw()
	push:start()

	--draw the background starting at top left (0, 0)
	love.graphics.draw(background, -backGroundscroll, 0)

	--draw the ground on top of the background
	love.graphics.draw(ground, -groundScroll, VIRTUAL_WIDTH)

	push:finish()
end
```

the `update(dt)` function updates the _starting point_ at which the picture is drawn onto the screen, and `draw()` function is the function that actually puts the image. Note that the x axis is the _negative_ of the `(back)groundScroll` values we got from the `update(dt)` function above, because we're essentially moving the image to the _LEFT_, and once the rightmost part of the screen reaches the rightmost end of the image, we loop back to 0.
![[Pasted image 20240614090711.png]]

---
Categories: [[Game Development]], [[CS50 - Game]]
References:
Created: 2024-06-14
