---
tags:
---
# Finite State Machines
Players, NPCs, or anything really, can be in multiple states. We can set flags to trigger each state. For example, when a player gets hit, we might want to put the player in a temporary "invulnerable" state, which can be triggered by the "hit" flag, and after the "timeout" flag for the invulnerable state is triggered, the player's invincibility stops. But what happens if multiple flags are triggered? how will we set the instance's state then? The simplest answer is to restrict anything to be in a single state only. This can be represented by what's called as a Finite State Machine (FSM).
![[FSM 2024-06-02 19.01.22.excalidraw.png]]
Above is a simple FSM for a Player. States are the ellipses. Text written on the arrows are the flags that trigger a transformation from one state to the other. We can see that There can be only one possible state at any given time, no matter how the flags are set.

In Godot, we can represent this using Enums as states.
```godot
enum {INIT, ALIVE, DEAD, INVULNERABLE}
```

---
Categories: [[Game Development]]
References:
Created: 2024-06-02
