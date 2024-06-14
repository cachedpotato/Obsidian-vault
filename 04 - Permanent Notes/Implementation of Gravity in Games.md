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

## Extending the Concept of gravity - Jumping
Now that we know how gravity works, how do we "jump?" jumping isn't just about y axis, it's also about the x axis. Think of a parabola:
![[Pasted image 20240614172545.png]]
Every frame, we update the player's position by updating it's x and y positional values, which is essentially just a vector operation.
Because the force of gravity only acts upon the y axis, it has no dependency on the change of x, meaning we can calculate them separately, like so:
```lua
JUMP_FORCE = -200
GRAVITY = 7
function love.keypressed(key)
	if key == 'escape' then
		love.quit()
	else if key == 'space' then
		DY = JUMP_FORCE

end

function love.update(dt)
	if love.keyboard.isDown('left') then
		characterX = characterX - CHARACTER_MOVE_SPEED * dt
	else if love.keyboard.isDown('right') then
		characterX = characterX + CHARACTER_MOVE_SPEED * dt
	end

	DY = DY + GRAVITY
	characterY = characterY + DY * dt
	if characterY >= (7 - 1)*TILE_SIZE - CHARACTER_HEIGHT then
		--we have hit the ground
		--stop falling and update acceleration to 0
		characterY = (7 - 1)*TILE_SIZE - CHARACTER_HEIGHT
		DY = 0
end
```

---
Categories: [[Game Development]], [[Physics Engine]]
References:
Created: 2024-06-14
