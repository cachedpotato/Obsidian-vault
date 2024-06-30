---
tags:
---
# PaperZD
`PaperZD` is a plugin, or rather an extension, of Unreal Engine's native 2D game plugin `Paper2D`. It simplifies the process of adding sound effects, and creating the animation flow by using [[Finite State Machines]]. There are three assets that comes with the plugin:

- Animation Sequence
- Animation Source
- Animation Blueprint

Animation Sequence is just data of flipbook and sound effects. Animation Source is the main asset to use to edit flipbook: where to add sound effects, where to [[Adding Sound Effects in UR|add sound effects]], etc. We can edit all the character/object related sprite source here, and call each animation as we see fit using the Animation Blueprint asset. The diagram below is a simple representation of these three assets:
![[Pasted image 20240628161824.png|550 x 700]]

## Setting up PaperZD
To use PaperZD, when we first create our character Blueprint, the blueprint class needs to be `PaperZD Character`:
![[Pasted image 20240628163005.png|500]]
Which has all the features of `PaperCharacter` with Plugin-related settings such as `Animation Component`, which we'll get to later.

Next, We need to create an `Animation Source` asset, which looks like this:
![[Pasted image 20240628162122.png]]
Personally think it looks a lot similar (and acts like one too) to a video editor, but moving on. Whenever we click the `Add New` button at the top right, a new `animation sequence` file will be generated automatically. At the bottom we can add "Notifications", where we can add things like sound effects, etc., at the exact frame we desire. 

Next, we need to create a `Animation Blueprint` Asset. We have two Graphs: `Event Graph` and `Animation Graph`. In the event graph, all we need to do to get things started is to `Get Owning Actor` and cast it to the character blueprint:
![[Pasted image 20240628162522.png]]
The [[Animation Graph]] is where the real fun of PaperZD lies, but that's for another node. For our character Blueprint to actually use this Animation Blueprint, we need to set as the `Component Class` under `Animation Component`:
![[Pasted image 20240628162755.png]]


---
Categories: [[Unreal Engine]], [[2D Game Dev]]
References:
