---
tags:
---
# Attack Hitbox
Attack animations are meaningless unless they have a hitbox that can actually detect and damage enemies. This note will cover only the very basics of creating a hitbox. We will also be utilizing PaperZD's Animation Source notifications for turning hitboxes on and off.

## Step 1. Creating Hitbox
This step is fairly simple. All we need to do is under the player (or parent) blueprint, we create a `Box Collision` componenet, name it `Hitbox` (or whatever you desire, really), and set its extent and location.
![[Pasted image 20240714172519.png]]
We also don't want the hitbox to be detecting collision for all object types. Set collision response to however we want the hitbox to be. One of the most basic response setup is to ignore everything except for the `pawn` class (which includes enemies and player):
![[Pasted image 20240714172728.png]]
Of course we will be dynamically changing hitbox responses, which is actually our next step.

## Step 2. Custom Toggle Hitbox function
As said before, we don't want the hitbox to be detecting for collision all the time. We only need this for attacking. What we need here is a custom function that can toggle the hitbox.
![[Pasted image 20240714173057.png]]
This can be done pretty easily. As input we will take a Boolean Value `Set Active`, and if this is set to true, we turn the collision on. To do this we use the `Set Collision Enabled` function, which works similar to `Set Collision Response` for changing the _response type_ of collisions, as shown in [[One-Way Platforms#^731ddc|one-way platforms]].

## Step 3. Creating Notifications for toggling hitboxes
There are multiple ways of using this function. We can just add this function in our `IA_Attack` event, but using it inside Animation Source is more manageable with notifies.
To do this, first we need to create a custom notify state.
![[Pasted image 20240714173519.png]]
Inside this blueprint, there are 4 overridable functions: 
- `OnNotifyBegin`: Run when notify begins
- `OnNotifyEnd`: Run as notify ends
- `OnNotifyTick`: Run every frame during the notification
- `GetDisplayName`: Change the notify name in animation source UI

Recall what we need to do: 
- When attack animation _starts_, we activate the hitbox
- When attack animation _ends_, we deactivate the hitbox

What we need to do with this override functions are clear.
![[Pasted image 20240714173840.png]]

![[Pasted image 20240714173821.png]]
using PaperZD's `Get Player Character` function, we can cast this to our parent blueprint (Enemies will also be using hitboxes) and call the `Set Hitbox Collision` function we created earlier to toggle our hitbox.

## Step 4. Using Notifications within Animation Source file
All we have left to do is actually use the notification we created earlier in our Animation Source file.
![[Pasted image 20240714174156.png]]
Notify States are _continuous_, so we can freely change the duration of this notification.

---
Categories: [[020-Game Development]], [[Collision Detection]], [[Player Attack]], [[PaperZD]]
References:
