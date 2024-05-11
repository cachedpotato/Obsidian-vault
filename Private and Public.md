---
tags:
  - Rust
links: "[[Rust]]"
---
# Private and Public
by default, all mods and its code is private. you must specify what should be public with the ```pub``` keyword.
```rust
mod front_of_house {
	pub mod hosting {
		fn add_to_waitlist() {}
	}
}

pub fn eat_at_restaurant() {
	//this throws compile time error
	crate::front_of_house::hosting::add_to_waitlist()
}
```

we made the hosting module public, but when we try to compile this it throws an error. that's because even if the module is public, its _contents_ are still set to private. for eat_at_restaurant() to be able to use the to_waitlist function, you must first make the function itself public as well:

```rust
mod front_of_house {
	pub mod hosting {
		pub fn add_to_waitlist() {}
	}
}

pub fn eat_at_restaurant() {
	//this throws compile time error
	crate::front_of_house::hosting::add_to_waitlist()
}
```

### structs and enums
you can make structs/enums within modules public, and for structs, just like anything else these are set to private by default.
```rust
mod back_of_house {
	pub struct Breakfast {
		pub toast: String,
		seasonal_fruit : String,
	}
	impl Breakfast {
		pub fn summer(toast: &str) -> Breakfast {
			Breakfast {
				toast: String::from(toast),
				seasonal_fruit: String::from("watermelon"),
			}
		}
	}

	//whereas impl within the module block CAN make use of
	//private values, other "regular" functions outside
	//the module cannot

	pub fn eat_at_restaurant() {
		let mut meal: back_of_house::Breakfast = \\
		  back_of_house::Breakfast::summer("wheat");

		meal.toast = String::from("Rye");
		//below will give error
		//as seasonal_fruite is a private value
		meal.seasonal_fruit = String::from("apple");
	}
}
```

however, for enums, if the enum is made public, then _all its variances are public as well_:
```rust
mod back_of_house {
	pub enum Appetizer {
		Soup,
		Salad,
	}
}

pub fn eat_at_restaurant() {
	let order1 = back_of_house::Appetizer::Soup;
	let order2 = back_of_house::Appetizer::Salad;
}
```

Nota that back_of_house is NOT set to public, but eat_at_restaurant() can still use the Appetizer enum, as that one IS public.
## References

Created: 2024-05-11