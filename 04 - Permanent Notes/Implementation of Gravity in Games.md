---
tags:
---
# Implementation of Gravity in Games
It's not an exaggeration to say platformers are defined by its buttery smooth controls and jumps. Super Mario Bros., the first ever platformer, had jumping as it's core mechanic after all. But how do we actually make characters jump?

We all know what gravity is. gravity is what pulls us down. Jumping essentially goes against this force of gravity for a brief period of time, making the object go up. However at some point, the gravity will catch up, and after reaching peak height, we'll fall back again.

## Simple implementation example

The plan is simple:
1) Have some constant `GRAVITY` set to some value
2) Have this constant multiplied to our `dy` every frame
3) If the user inputs `jump`, temporarily set the `dy` value to a _NEGATIVE_ value (remember: games have y axis flipped)

```lua
Bird = Class{}

function Bird:init()
	self.x = VIRTUAL_WIDTH/2
	self.y = VIRTUAL_HEIGHT/2
end

local GRAVITY = 9.8 --9.8m/s^2 anyone?

function Bird:update(dt)
	self.dy = self.dy * GRAVITY

	if love.keyboard.wasPressed('space') then
		self.dy = -5
	end

	--update the actual position
	self.y = self.y + self.dy
end
```


---
Categories: [[Game Development]], [[Physics Engine]]
References:
Created: 2024-06-14
