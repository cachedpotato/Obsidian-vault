---
tags:
---
# Hitstun
When player/enemies get hit, there must be at least some indication. One of the most universal ways of doing so is by adding a hit-stun animation. Having a good hit-stun system can vastly improve player experience. We want our attacks to have some weight, after all. 

Just like [[Attack Hitbox|attack animations]], we can get hit at any point in time. We can use animation overrides or jump nodes, but for this case we'll be using jump animation, as we want to move straight to idle animation rather than back to previous animation.

## Step 1. Creating Jump Nodes
This process is virtually identical to the [[The Death-Touch|Player Defeated animation]] here, but to reiterate Within our `AnimGraph`, create a jump node and connect it to an animation node for Stun.
![[Pasted image 20240714190937.png]]
Make sure the actual stun animation itself is inside our Animation Source file.

## Step 2. `IsStunned` State and `Faction`
We next need to create a value for storing our stun state. We should be in the stun state for only a certain period of time, and go back to normal. Having a Boolean value for managing states (or enums for that matter) will make things a lot easier.

We will also need an integer value `Faction` to indicate whether the object being hit is either the player or the enemy if we have the hitbox related functions set up in the parent blueprint. The details will be explained in the next step.

## Step 3. `ReceiveAttack()` function
Hitstun happens when hitbox overlaps with a pawn instance. Therefore, we need to create a function that handles the hitstun logic and connect it to `Event BeginOverlap (hitbox)` event.
![[Pasted image 20240714191805.png]]
Before we get into the function itself, we first need to talk about the whole logic with `faction`. Currently we're in parent blueprint that handles _both_ player character and enemy. so this hitstun event will happen for both classes. We don't want the player to hit themselves, and the same thing goes for enemies as well. By having an integer `Faction`, and setting it to different values for player and enemy, we can get solve this issue.

Essentially the logic is: "Go into hitstun only if the hitbox overlaps with a pawn instance of different faction".

Now, let's move into the `ReceiveAttack()` function. This function must do the following:
- Set `IsStunned` to true
- Set animation to the hitstun animation
- Reset `IsStunned` to false after a set point of time

To do this, we need two function calls:
- `Jump to Node` function from PaperZD (to call the jump node)
- `Set Timer By Event` node for the hitstun delay
![[Pasted image 20240714192519.png]]
Since this is a function, we can't call the `delay` node, hence the need for `set timer by event`. One cumbersome aspect of this is that we need to create a separate function for resetting the `IsStunned` value so that we can create an event by function call and connect it to `Set Timer By Event` Node, like so:
![[Pasted image 20240714192656.png]]

## Step 4. Going back to idle animation
So far we have the animation logic set up for going _into_ hitstun, but not _out of_ it. All we need to do is add a simple check to the `Stunned -> idle` state logic if we're out of the `IsStunned` state:
![[Pasted image 20240714192832.png]]

## Step 5. Disable movement during hitstun
During hitstun, the player should not be able to move. in `IA_Move`, we need to add a branch condition that checks if we're able to move, such as:
- If we're in a hitstun
- If we're attacking
- If we died
![[Pasted image 20240715200350.png]]


---
Categories: [[Player Attack]], [[020-Game Development]], [[PaperZD]], [[Attack Hitbox]]
References:
