---
tags:
---
# Ability System
This note will not cover the system itself, rather an implementation method (so the mechanism) of an ability system. Abilities can be stored as an Enumerable, then as players unlock certain abilities, we can add those to the enumerable array. The way of unlocking abilities can vary, but one of the simplest ways is to get an item. In short, what we need are:
- An Item that gives abilities
- An Enum of abilities
- An array that can store unlocked abilities (in character BP)
- In item BP - pickup logic
- In player BP - ability logic
- + Maybe Material blueprint for customizing items
![[Pasted image 20240716090503.png]]
## Setting Up Ability Item
Inside Ability Item blueprint, we should have a list of unlockable items in the form of a list or an enumerable. In this case, we'll be using enums. Also, we need to add some sort of logic for the player to "pick up" the item.

### Ability Enumerator
Before we create the item blueprint, first we create an Enumerable blueprint. From the main menu, right click and go to `Blueprint > Enumeration`:
![[Pasted image 20240716091134.png|500]]
The UI is quite simple. Add Abilities we want the players to be able to unlock.
![[Pasted image 20240716091205.png]]
### Ability Item Blueprint
Now, create a basic `Actor` blueprint. Creating the visuals/graphics for items are a whole another can of worms that we won't be getting into here, but For the purpose of this note, creating a simple `Sphere` object would suffice.

While we can use the collision for the sphere itself, for a better player experience we may want the collision box to be bigger than the sphere itself. What we should do then, is to
- Remove collision for the sphere object
- Create a new `BoxCollision` object that will have the collision box
![[Pasted image 20240716091724.png]]
The collision should not interact with anything except for the player (`pawn`) class, so we set the collision response like so:
![[Pasted image 20240716091812.png|550]]

Next, we create an Enumerable variable abilities, and call the Enum blueprint we created earlier:
![[Pasted image 20240716091953.png]]
The ability type will vary depending on the item instance/child blueprint.

While there are a bunch of things we can do with the item blueprint, one of the most basic thigs it must to is to have a pickup logic. Once the hitbox collides with the player, it should give the stored ability to the player and destroy itself. 
![[Pasted image 20240716092159.png]]
We can see that after we call the `Event Begin Overlap`, we call a function from the character blueprint `GainAbility()`. What to do with the ability will be processed within our character blueprint. After this, the `DestroyActor` clears the item instance.

## Player Blueprint Function
Within the player blueprint, we also need to add the ability variable, but this time as an _array_. This can be done by first adding the Enum variable, then in the `Variable Type` options selecting `Array`.
![[Pasted image 20240716092556.png]]
Now we need to create the function for handling abilities. This function should:
- Add gained abilities to list (_NO DUPLICATES_)
- Define what each ability does
![[Pasted image 20240716092814.png]]
This is a bare-bone implementation of that function. It takes the Ability Enum as input (so that we can call it in our item blueprint) and we use the `Add Unique` node to add to player ability array.

We also have a `Selector`, that creates a multi-arm branch based on gained ability. For example, if the ability was `DoubleJump`, we will set the `Max Jump Count` to `2` (which is a native function in UR!)



---
Categories: [[Unreal Engine]], [[020-Game Development]]
References:
