---
tags:
---
# Carrying Over variables through Game Instance in Unreal Engine
The variables we store in blueprints do not carry over when we open up/load a new map. For values that need to be reset it's fine, but if we have data that needs to be transferred over (such as [[Ability System|abilities]]), we need to store and load in some way. To do this, we need to use a separate blueprint, called `Game Instance`.
## Setting Game Instance
Setting up game instance is fairly easy. First, we create a new blueprint of class `GameInstance`.
![[Pasted image 20240717113219.png|500]]
This next part is crucial. Under `Maps & Modes` project settings, we need to set the `Default Game Instance` to the `GameInstance` blueprint we created:
![[Pasted image 20240717113401.png|500]]

## Storing Values through Game Instance
Now, we need the Game Instance to actually store values. This process is quite easy, albeit a bit tedious. First we need to list every single data we want to transfer and create a new variable (of the same type) inside the game instance. For example, If we want to store an integer value `MaxJumpCount`, which is already in our character blueprint, we also need to make an integer value inside the game instance folder. It's recommended to use the exact same name.
![[Pasted image 20240717113655.png]]
Now, inside our character blueprint, we need to create a function that will actually store the values. Below is an example of such function:
![[Pasted image 20240717113911.png]]
To store values, we first need to get the Game Instance, cast it to our custom game instance blueprint, and store values there. This can easily be done by the `SETTER`.
Finally, we need to set _when_ to store. This would be when we're [[Level Transition in Unreal Engine|moving to next level]], so call this function right before we load next level.
![[Pasted image 20240717112624.png]]
## Loading Values
Storing values inside the game instance does not automatically transfer the data over to the player character. Whenever a new map is loaded, the character constructor is called. Therefore, inside the constructor, we need to get our game instance once again, but now the direction will be the _opposite_: instead of storing data from player blueprint to game instance, setting player blueprint data from game instance.
![[Pasted image 20240717114435.png]]


---
Categories: [[Unreal Engine]], [[Level Transition in Unreal Engine]], [[Blueprint Class]], [[Blueprint]]
References:
