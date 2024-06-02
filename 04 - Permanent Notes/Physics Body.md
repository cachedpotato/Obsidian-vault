---
tags:
---
# Physics Body
Physics in gaming is basically split into two parts: Collision detection and Collision Response. When two Collision Boxes Collide, some physics mechanism can occur, and we can set those up using physics bodies.

There are three types of body that Godot natively provides for dealing with physics:
1) StaticBody2D: Does not move, but provides collision detection. Is normally used for environmental scenes.

2) RigidBody2D: Provides both collision detection and native physics simulation. Does not need user-generated physics logic.

3) CharacterBody2D: Provides Collision detection but does not provide simulation. Collision response must be done manually through the script.

They all have their use cases, so learning when to use what body is paramount for game development.

We can set global attributes that will apply to all bodies within the `Project Settings` panel.

## Advanced Options
- Linear Damp: the rate of dampening (decreasing) of forward speed
- Angular Damp: the rate of dampening of angular speed

## RigidBody2D
there are multiple attributes that lets us customize behaviors. examples include:
- Mass
- Friction
- Bounce: Think of bouncy balls.

### `_physics_process` function
the `_physics_process` function processes force and torque using delta. When using physics body, we _MUST_ call here functions and/or movement related stuff. For example, if we're trying to control a spaceship that rotates and goes forward with a given thrust value, we may do something like this:
```gd
func _physics_process(delta):
	constant_force = thrust
	constatnt_torque = rotation_dir * spin_power
```

### `_integrate_forces` function
RigidBody2D document states that its position or linear velocity remain unchanged, which can be trouble some because, well, we want to move things. Luckily, we have the `_integrate_forces` function that lets us have access to `PhysicsDirectBodyState2D` that contains a bunch of information about the body's physics state.
```gd
func _integrate_forces(physics_state):
	var xform = physics_state.transform;
	xform.origin.x = wrapf(xform.origin.x, 0, screensize.x)
	xform.origin.y = wrapf(xform.origin.y, 0, screensize.y)
	physics_state.transform = xform
```
this function lets the object wrap around the screen.


---
Categories: [[Nodes in Godot]]
References:
Created: 2024-06-02
