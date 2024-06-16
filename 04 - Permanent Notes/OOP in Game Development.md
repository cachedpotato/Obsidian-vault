---
tags:
  - NeedWork
---
# OOP in Game Development
Games are essentially a giant simulation of objects that interact with each other. This is why when we create scripts for games, it's best to implement the Object Oriented Programming, at least to some degree.

An object can hold many variables, including states, and can be manipulated using methods. The Following is a simple diagram of the `Player` class and its C++ implementation:
![[Pasted image 20240614042129.png]]
```C++
enum State { 
	bool alive,
	bool dead,
	bool invulnerable
	bool init,
} State;

class Player {
	int self.lives;
	int self.hit_points
	State self.current_state;

	void take_damage(self, int* damage) {
		self.hit_points -= damage;
		if (self.hit_points < 0) {
			self.lives -= 1;
			self.state = invulnerable;
			self.hit_points = 100;
		}
	}

	void game_over(self) {
		if (self.current_state == dead {
			//something something ...
		}
	}
}
//snip
```


---
Categories: [[020-Game Development]]
References:
Created: 2024-06-14
