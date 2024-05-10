---
tags:
  - Rust
links:
---
# Structs
at first glance structs use the same as structs in any other functional language:
```rust
struct User {
	active: bool,
	username: String,
	email: String,
	sign_in_count: u64,
}

fn main() {
	let mut user1 = User {
		active: true,
		username: String::from("mango"),
		email: String::from("mango@no_reply.gmail.com"),
		sign_in_count: 0,
	}

	user1.sign_in_count += 1;

	let user2 = User {
		email: String::from("alias@shady.com"),
		..user1
	} //every other field follows user1
}
```

note that for a struct instance to be mutable, the **ENTIRE** instance (all fields) must be mutable! so no string slices! You can also create new struct instances using other instances. Rust's borrow checker also works here as well. Since we moved a String from user1 to user2, user1 is no longer available. However, if we only used user1's active and sign_in_count fields, because both are in the stack, user1 would still be valid.

## field init
Say we want to make a constructor. In such case, we often find ourselves naming our parameters the same as the field names:
```rust
fn build_user(username: String, email: String) -> User {
	User {
		active: true,
		username,
		email,
		sign_in_count: 0,
	}
}
```
as we can see, we just wrote ```username, email``` and not ```username: username, email:email,```. this is because rust has what's called a field init shorthand.

## creating new types and unit structs
```rust
struct Color(u8, u8, u8); //unnamed fields + tuple struct > new type
struct Point(u8, u8, u8);
struct Unit; //unit struct

fn main() {
	let color1 = Color(0, 0, 0);
	let point1 = Point(0, 0, 0); //same value, different type
	let unit1 = Unit;
}
```

for Structs to be able to be printed in its entirety, we need to either [[Implementation|implement]] the debug trait or the Display trait, like so:
```rust
#[derive(debug)]
struct Rectangle {
	height: u32,
	width: u32
}

fn main() {
	let rect = Rectangle {
		height: 30,
		width: 50
	}
	println!("{:?}", rect) //Rectangle{height: 30, width: 50}
	println!("{:#?}", rect) //prints as below:
	//Rectangle{
	//height: 30,
	//width: 50
	//}

	//now that Rectangle has debug trait, this is possible
	dbg!(&rect);
}
```
## References

Created: 2024-05-10