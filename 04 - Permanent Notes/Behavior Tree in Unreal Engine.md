---
tags:
---
# Behavior Tree in Unreal Engine
Using behavior tree, we can change enemy behavior based on custom conditions, just like a tree. The base UI looks like this:
![[Pasted image 20240715130052.png]]
Everything starts from root, and using composites and tasks (explained below), we can create very complex AI.
## Composites
Composites are logic "types" of the node. Some branches can be done in a sequence, whereas others are selected, etc.
![[Pasted image 20240715130255.png]]
There are three types of composites
1) Selector: From child nodes, select only one.
2) Sequence: Selects child nodes in a set order, creating a sequence.
3) Simple parallel: Run child nodes simultaneously
## Tasks
Tasks are things we can let our enemies do without creating logic for it ourselves, such as following the player. 
![[Pasted image 20240715130608.png]]
Notable Tasks include:
- Move To: Move to a certain Key class defined in [[Blackboard in Unreal Engine|blackboard]] 
- 

---
Categories: [[Enemy AI]], [[Unreal Engine]]
References:
