---
tags:
---
# Enemy Attack
If Enemy is within range, it should try to attack the player. Of course we can add a LOT more nuance into it than just "if close attack", but that's the basics of it. Even doing just this requires a lot of work so let's get right into it.

## Step 1. Creating Behavior Tree Task
While we can create attack event within our enemy blueprint, it can be easier to manage with behavior trees. One great thing about behavior trees is that we can create custom tasks, with custom functions.
In the main menu, click `Blueprint Class > BTTask_BlueprintBase` to create a new task blueprint.
![[Pasted image 20240715194355.png|600]]
Similar to the [[Attack Hitbox#^8b0a82|override-able functions in notifies]], we will be using function overrides, specifically `Receive Execute AI`:
![[Pasted image 20240715194601.png|600]]

## Step 2. Setting up attack animation
The task here takes care of the attack animation, so we can apply what we did for [[Attack Animation and Animation Overrides|player attacks]], which is to
- Override Animation to attack animation
- Set `IsAttacking` to true when the animation starts
- Set `IsAttacking` to false when the animation ends
- Add condition for when the enemy's able to attack

In addition to this, we also need to take care of node `Finish Execute` to notify the behavior tree that the task is done. If the attack task is cancelled (or is not eligible for attacking to begin with), it we should end task with `Fail` status, and if it connects, end with `Success` status.

Seems pretty wordy, but in practice it's quite simple.
### 1. Branch Condition
![[Pasted image 20240715195106.png]]
The `CanAct()` function returns True if the enemy can move into the next animation/status. The details can be found [[Flipping Enemy Sprites#^729e8b|here]]. 

### 2. Play Animation and Exit
![[Pasted image 20240715195250.png]]

## Step 3. Behavior Tree
Now it's time to actually implement the task we've just created. Since tree nodes are executed based on branches and priorities, order matters. For a basic attack pattern, we can just let the enemy attack whenever the player's within reach. So the priority must be: 
1) Attack (MOST IMPORTANT)
2) Move to Player
3) Wait
![[Pasted image 20240715195554.png]]
By using `add decoration`, we can set enemies to attack based on distance from player. click `add decoration > is at location`, and set it up like so:
![[Pasted image 20240715195703.png]]
Make sure the `Key` is set to `AttackTarget`. The `Acceptable Radius` is the distance _FROM_ the target, not from the enemy pawn, so don't mix up the point of origin!

## Step 4 - Cleanup and removing overrides
Now enemies will be able to attack, but there are some things we need to clean up. The most important thing is to check stun length, and see if player (or enemy) gets in a stunlock. This can be adjusted by changing the [[Hitstun]] time.

Next, we need to make sure the attack animation is cancelled when it receives damage/dies, so that the interactions don't look as janky. Basically, we're overriding the override. This can be achieved using `Stop all animation overrides`:
![[Pasted image 20240715200137.png]]

---
Categories: [[Enemy AI]], [[Behavior Tree in Unreal Engine]]
References:
