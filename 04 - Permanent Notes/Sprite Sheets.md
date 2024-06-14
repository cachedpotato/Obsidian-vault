---
tags:
---
# Sprite Sheets
A sprite sheet is a collection of sprites that is used to load, well, sprites, into the game. While it is possible to have a separate sprite file for everything, this can get quite messy as the game's scale grows. instead, especially if the game is mostly rectangular, we can group some (or all) sprites into a sprite sheet and load certain portions of that.

An example sprite sheet looks like this:
![[Pasted image 20240614110247.png|500]]
This is a sprite sheet for breakout type game (where you move the platform around to bounce the ball and break bricks). Here we see various platforms, bricks, hearts, and other cool stuff. This is good and all, but how do we load things accordingly? This is just one giant PNG file, if we just load it we would have this giant blob of sprites.

## Quads
We can use the concept of `Quads` to separate this PNG file into multiple sections, and load a specific quad for some object.
![[Pasted image 20240614110627.png|500]]
Quads are just glorified rectangles. to get a certain quad, we use our Game Engine of choice's `get Quad` function.
```lua
love.graphics.newQuad(x, y, width, height, dimensions)

love.graphics.draw(texture, quad, x, y)
```


---
Categories: [[Game Development]], [[CS50 - Game]]
References:
Created: 2024-06-14
