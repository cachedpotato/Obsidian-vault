---
tags:
---
# Tile Maps in UR
Using Tile sheet/Sprite sheets as brush, we can create maps. A map made out of tiles is called, well, tile maps, and here's how to create one in Unreal Engine.

## Step 1. Tile sheet to Tile Set
First, We need to create the proverbial "paint" of the tile map. This can be done by using `Create Tile Set` from `sprite actions`:
![[Pasted image 20240628181627.png]]


## Step 2. Adding Collision
Next, we need to add collisions to tiles that are going to be used as floors/platforms. Double click the newly created Tile Set, and set the `Tile Size` to the appropriate amount. Then, we need to start painstakingly adding collision boxes _one by one_. To do this click "Add Box" and select parts that need collision. Make sure to click the `Colliding Tiles` on the top left to actually see where it's being placed:
![[Pasted image 20240628182004.png]]

## Step 3. Creating Tile Map
Right click the tile set and select `create tile map`
![[Pasted image 20240628182151.png]]
The main Tile map menu looks similar to any other drawing tools like Photoshop, Gimp, etc., with layers and stuff, but I won't get into details here. 
![[Pasted image 20240628182514.png]]
Make sure to have separate layers for foreground/background, etc., so that we don't get nasty artifacts, and also _turn off collision check for all layers except for the foreground_ by un-checking the `layer-collides` option

---
Categories: [[020-Game Development]], [[2D Game Dev]], [[Unreal Engine]]
References:
