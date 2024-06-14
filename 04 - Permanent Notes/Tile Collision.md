---
tags:
---
# Tile Collision
If we design levels using tiles, our measurement can be "quantized". Meaning, we don't need to look at some continuous value down to its decimal points, but instead, just check if we're above/below/between a certain tile. This can be done simply by dividing the object's current x and y axis, and dividing them by the tile width and height.
![[Pasted image 20240614190214.png|500]]
Think of tile collision checking for ceilings. we don't really need the exact coordinates, we just need to see what tile our corners are interacting with. As mentioned before, we can get which tile a certain coordinate is in by dividing it by tile size:

```lua
function TileMap:pointToTile(x, y)
	if x < 0 or x > self.width * TILE_SIZE or y < 0 or 
		y > self.height * TILE_SIZE then
		return nil
	end

	return self.tiles[math.floor[y / TILE_SIZE + 1 ]
		[math.floor(x / TILE_SIZE) + 1]]
end
```
the first `if` case is for figuring out if the player's off screen. the last `return` statement shows that we're returning a tile from a tile matrix, and the indices are acquired by `math.floor(x/TILE_SIZE)` operation. We can then pass this to our collision detection logic.

There is one small thing we need to consider. because the tiles are fixed size, it is very possible that our upper left corner and our upper right corner of the collision box points to different tiles, as depicted in the picture above. Therefore, we need to check _PAIRS_ of corners for collision detection.

- for ceiling: upper left and upper right
- for floor: lower left and lower right
- for wall (right): upper right and lower right
- for wall (left): upper left and lower left

---
Categories: [[Game Development]], [[Collision Detection]], [[CS50 - Game]]
References:
