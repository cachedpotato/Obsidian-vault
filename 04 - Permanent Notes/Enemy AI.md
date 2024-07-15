---
tags:
---
# Enemy AI
In Unreal Engine, These three things acts as a full set for enemy AI:
- [[Blackboard in Unreal Engine|Blackboard]] : Used to set keys
- [[Behavior Tree in Unreal Engine|Behavior Tree]]: Used to set behavioral patterns
- [[Controlling Enemy AI|AI Controller]]: Used to control AI/Define behavior functions
Below is a simple diagram showing the relationship of the three
![[Pasted image 20240715124343.png]]

With these three, we can achieve the following:
- [[Player Aggro]]
- [[Enemy Attack]]
- ... And many more!


## Enemy AI setup
Setting things up is as easy as creating all three blueprint classes and connecting them together.

### Step 1. Create Blackboard
From `Artifical Intelligence`, click `Blackboard`.
![[Pasted image 20240715125056.png|500]]
The UI looks like this:
![[Pasted image 20240715125029.png]]
### Step 2. Create Behavior Tree
From `Artificial Intelligence`, click `Behavior Tree`. Within the UI, we must set the blakcboard to the one we've just created:
![[Pasted image 20240715125316.png]]
### Step 3. Create AI Controller
From `Blueprint Class`, click `AI Controller`. Within the event graph, we need to initialize both the blackboard and the behavior tree.
![[Pasted image 20240715125517.png]]

### Step 4. Enemy Blueprint setup
From our Enemy blueprint, within the `Pawn` section, there are two things we want to change.
1) AI Controller: Set it to the AI Controller blueprint we created.
![[Pasted image 20240715125726.png]]
2) Auto Possess AI: By default it's `Placed in World`. This means any spawned enemies won't have the AI controller set up properly. Change this to `Placed in World or Spawned`.
![[Pasted image 20240715125812.png]]

---
Categories: [[Unreal Engine]], [[020-Game Development]]
References:
