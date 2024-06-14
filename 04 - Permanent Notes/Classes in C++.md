---
tags:
---
# Classes in C++
C++ is a superset of C, meaning it has all the features of C and then some. where do this extra stuff come from?
Whereas C is mainly a functional programming language, C++ supports Object-Oriented Programming, by using `class`es and inheritance. Let's take a closer look.

```C++
#include <string>
#include <vector>
class Human {
public:
	int friend_count;
	std::string name;
	std::string phone_number;

	void sayHi(Human to, Human from);
	bool isLoner(self) {
		if (self.social_tier() < 5) {return true;}
	}
private:
	int social_tier(self);
	int total_earnings(self);
}
void Human::sayHi(std::string to, std::string from) {
	std::cout << from.name << "says hi to " << to.name << std::endl;
}
//--snip
```

Like [[Private and Public]] in Rust, C++ also lets us control what is shown and what is hidden to users of this class. The difference here is that whereas in Rust everything defaults to `private`, in C++ everything defaults to `public`.

We can also see that class methods can be both defined _internally_ inside the class definition or _externally_. However, we have to make sure to add the `className::methodName` syntax when we define functions externally.

## constructor and destructor
classes in C++ can have custom constructor and destructor with the following functions: `ClassName()` and `~ClassName()`:
```C++
class Human {
public:
	Human(std::string name, int friend_count) {
		name = name;
		friend_count = friend_count;
		phone_number = "";

		std::cout << "Bless thy soul " << name << std::endl;
	}

	~Human() {
		std::cout << self.name << " had a good life." << std::endl;
	}
}

int main() {
	Human Reimu = Human("Reimu", 1231);
	Human::sayHi(Reimu, Marisa);
	Human Marisa = Human("Marisa", 1231);
}
```

```bash
$./program.o
Bless thy soul Reimu
Bless thy soul Marisa
Marisa says hi to Reimu
Marisa had a good life
Reimu had a good life
```
Note that the latest object created is freed first because as we've talked before, computer stores memory using [[Stack|stacks]], and stacks are LIFO. Also Note that destructors are called automatically when the object goes out of scope.

---
Categories: [[C/C++]]
References:
