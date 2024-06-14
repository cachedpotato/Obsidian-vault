---
tags:
---
# Procedural Generation
Procedural Generation is one of the more hot topics in game development. Procedural generation lets computer algorithms create levels by themselves, without any external human input. Popular games that implement procedural generation include [[Dead Cells]] and many other [[Roguelike]] genre games.

## Example: Platformer
How can we implement procedural generation for platformers? A very basic implementation would be having flags for certain conditions, and when those flags are set to `true`, we create a "column" of tiles that corresponds to that tag. For example, the columns can have the type:

- flat (base case)
- pillar, where we have pillars player have to jump over
- chasm, where there's nothing in the column

We can also add item blocks or enemies using flags, but let's focus on the basics for now. a pseudocode would look something like this:
```
FLAG is_pillar
FLAG is_chasm

function generate_column()
	is_chasm = math:rand(10) == 2 ? true : false
	if chasm {
		return --do nothing
	}

	is_pillar = math:rand(5) == 1 ? true : false
	if is_pillar {
		from ground_level to pillar_height:
			draw(tile[id.pillar])
	}

	--base case - flat level
	from end_of_screen to ground_level:
		if ground_level:
			draw(tile[id.topped]) --grassy blocks at top
			return
			
		draw(tile[id.base])
end
```
By generating a random value, we create a random chance of that column having a certain type of column. Note that in this implementation, `chasm` types are intentionally done first because it requires some sort of early return. Also, both flat and pillar columns must generate blocks from the bottom of the screen to ground level at minimum.

As mentioned in [[Tile Maps]], we can assign `id` to tiles, so that we can bring a certain type of tile when conditions are met. Here, we bring `topped` tiles, where the tiles have grass, for ground height tiles, to generate something that looks like this:
![[29feedaa5cff8e2b7fa479f3350bcb91.jpg|500]]
See how all tiles that have nothing directly above have grass on them? this is what the code does above, just for the ground level.


---
Categories: [[Game Development]], [[CS50 - Game]]
References:
https://i.pinimg.com/originals/29/fe/ed/29feedaa5cff8e2b7fa479f3350bcb91.jpg
