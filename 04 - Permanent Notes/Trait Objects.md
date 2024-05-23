---
tags:
---
# Trait Objects
Recall the time where, to store multiple types in a vector, we did a workaround with enumerations, like so:
``` rust
enum Workaround {
	Int(i32),
	Float(f64),
	String(String),
}

fn main() {
	let v: Vec<Workaround> = vec![
		Workaround::Int(3),
		Workaround::Float(3.1),
		Workaround::String(String::from("sneaky")),
	];
}
```
This is definitely useful, but there comes a time where we want to expand the available types. We can always add variants to the enumeration, but better than that, we can use trait objects.

Trait objects are literally that: objects with traits. to define it, we need the following:
- a pointer to the object (reference, box, etc.)
- the ```dyn``` keyword
The necessity for the latter is quite obvious - we are trying to accept _all types with a given trait_.

## Example of trait object
Let's say we're creating a GUI library. To be a GUI component, it needs to be able to "draw" things to the screen. Let's make that as a trait, and let various GUI elements implement this.
``` rust
pub trait Draw {
	fn draw(&self);
}

pub struct Button {
	width: u32,
	height: u32,
	label: String,
}
impl Draw for Button {
	fn draw(&self) {
		println!("A {} by {} button with label {}", self.width, self.height, self.label);
	}
}

pub struct SelectBox {
	width: u32,
	height: u32,
	selection: String,
}
impl Draw for SelectBox {
	fn draw(&self) {
		println!("A {} by {} selection box for {}", self.width, self.height, self.selection);
	}
}
```
Now, we define a ```Screen``` that can have multitude of GUI components. 
``` rust
pub struct Screen{
	components: Vec<???>,
}
```
Hang on a second, vectors can't hold multiple types! How are we supposed to add Both button and selection box? why, with trait objects of course!
```rust
pub struct Screen {
	components: Vec<Box<dyn Draw>>,
}
```
Note that we both
- have a pointer ```Box<T>```,
- the ```dyn``` keyword for the vector to accept the trait object

Now let's make an actual use case.
``` rust
pub struct Screen {
	components: Vec<Box<dyn Draw>>,
}
impl Screen {
	fn run(&self) {
		for component in self.components.iter() {
			component.draw();
		}
	}
}
```
in main.rs:
``` rust
use gui::{Button, SelectBox, Screen};
fn main() {
	let button_1: Box<Button> = Box::new(Button{
		width: 20,
		height: 20,
		label: String::from("random label"),
	});
	let box_1: Box<SelectBox> = Box::new(SelectBox{
		width: 30,
		height: 50,
		selection: String::from("random selection"),
	});
	let screen: Screen = Screen {
		components: vec![
			button_1,
			box_1,
		],
	};

	screen.run();
}
```
Results:
```
A 20 by 20 button with label random button
A 30 by 50 selection box for random selection
```

## Comparison with trait bounds
One might think we can just use the trait bounds to get the same result:
``` rust
pub struct Screen<T: Draw> {
	components: Vec<T>,
}
impl<T> Draw for Screen<T>
where
	T: Draw,
{
	fn run(&self) {...}
}
```
However, there is one _CRUCIAL_ difference - this version _CANNOT_ hold multiple types! We can only hold either the Button or the Selection Box, but never both.



---
Categories: [[Traits in Rust]]
References:
Created: 2024-05-23