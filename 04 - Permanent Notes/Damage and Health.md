---
tags:
---
# Damage and Health
Unless we're using the dreaded [[The Death-Touch|touch of death]], we will have some sort of health system (or hit point system, whatever we want to call it) that keeps track of our maximum health and goes down whenever we take damage. This is easily done by adding a `MaxHealth` and `CurrentHealth` float value to our player/pawn class.

## Initial setup
At the start, the `CurrentHealth` should be the same as the `MaxHealth`. Rather than tracking the default value of both variables, we can just set our `CurrentHealth` as our `MaxHealth` at `Event Start`.
![[Pasted image 20240714233211.png]]

## Adding Death animation
Now that we have health set up, we add a `Death` animation and add the logic to the `ReceiveAttack()` function. Just like [[Hitstun|hit-stuns,]] since we can die at any point, we'll be using jump nodes. 
![[Pasted image 20240714234146.png]]

We will also update the `ReceiveAttack()` animation similar to:
```C++
void ReceiveAttack(float Damage) {
	CurrentHealth -= Damage;
	if (CurrentHealth <= 0) {
		GetAnimInstance.JumpToNode("JumpDead");
		CapsuleComponent.SetCollisionEnabled("NoCollision");
		//additional logic..
		return;
	}
	//if HP > 0 (alive) we get stunned instead;
	IsStunned = true;
	GetAnimInstance.JumpToNode("JumpStun");
	SetTimerByEvent(ClearStun, StunTime);
}
```

![[Pasted image 20240714233836.png]]

![[Pasted image 20240714233903.png]]


---
Categories: [[Player Attack]], [[020-Game Development]]
References:
