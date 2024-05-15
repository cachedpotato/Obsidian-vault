---
tags:
---
# Testing in Rust
Tests are Rust functions that verify your non-test code is functioning. Whereas in binaries where you can just run main to figure out if it's working properly, in library crates you may want to make test cases.

## Three actions of testing
For proper testing, perform these three actions:
- Set up any needed date or state
- Run the code you want to test
- Assert the results are what you expect

## Anatomy of a test function
``` rust
//the function we want to test
pub fn add(l: usize, r: usize) -> usize {
	l + r
}

#[cfg(test)]
mod tests {
	use super::*; //setup

	#[test] //functions with this trait will be tested
	fn adder_test() {
		let result = add(2, 2); //running the code
		assert_eq!(result 4); //asserting results are as expected
	}
}
```
the ```#[cfg(test)]``` indicates modules with this attribute will compile and run _ONLY WHEN YOU RUN CARGO TEST_. cargo build won't compile this module. 

the ```assert``` family of macros will panic if it gets an unexpected result. For example, if this add function returned a 5, the test will panic. To actually test, you need to do ```cargo test```. 

sometimes, it's easier or even more useful to make test cases where it fails:
``` rust
//...
#[cfg(test)]
mod tests {
	use super::*;
	
	#[test] //functions with this trait will be tested
	fn adder_test() {
		let result = add(2, 2); //running the code
		assert_eq!(result 4); //asserting results are as expected
	}
	
	#[test] 
	fn panic_test() {
		let result = add(3, 2);
		assert_eq!(result, 7); //this will panic
	}
}
```
...this is a horrible example, but you get the gist.

## Checking results with assert! macro
as mentioned above, you can assert results match with your expectation with the ```asert``` family of macros.
``` rust 
pub struct Rectangle {
	height: usize,
	width: usize,
}

impl Rectangle {
	fn can_hold(&self, another: Rectangle) -> bool {
		self.height > another.height && self.width > another.width
	}
}

#[cfg(test)]
mod tests {
	#[test]
	fn larger_holds_smaller() {
		//setup
		let bigger: rectangle = rectangle {
			height: 10,
			width: 20,
		}
		let smaller: rectangle = rectangle {
			height: 5,
			width: 10,
		}
		//running the function and asserting expected results
		assert!(bigger.can_hold(smaller)); //assert! checks bool
	}
	
	#[test]
	fn smaller_cannot_hold_larger() {
		//setup
		let bigger: rectangle = rectangle {
			height: 10,
			width: 20,
		}
		let smaller: rectangle = rectangle {
			height: 5,
			width: 10,
		}
		//running the function and asserting expected results
		assert!(!smaller.can_hold(bigger)); //assert! checks bool
	}
}
```
reminder that the ```!``` is the NOT operator.

## useful macros
Here are some of the macros that are really useful for testing
1) assert!
``` rust
assert!(this_test_result(in1, in2) == expected_output);
```
checks bool. for custom error messages, add additional arguments
``` rust
#[test]
fn greeting_contains_name() {
	let result = greeting("Carol");
	assert!(
		result.contains("Carol"),
		"the message did not contain the name Carol, but instead had {}",
		result
	)
}
```
the second part of assert is pretty much the same as ```println!```.

2) ```assert_eq!/assert_ne!```
``` rust
assert_eq!(add(2, 2), 4);
assert_ne!(add(2, 3), 6); //opposite of assert_eq!
```

## Checking for panics: ```should_panic```
As important it is to check your test cases are returning expected values, it's also as important to check your program DOES PANIC in cases where it should. To test such cases, add the should_panic attribute. You can even add custom error messages!

``` rust
pub struct Guess {
	value: i32,
}

impl Guess {
	pub fn new(value) -> Guess {
		if value < 1 || value > 100 {
			panic!("Guess over 100");
		}
		Guess {value}
	}
}

#[cfg(test)]
mod tests {
	#[test]
	#[should_panic(expected = "less than or equal to 100")]
	fn greater_than_100() {
		Guess::new(200);
	}
}
```

## using Result in Tests
besides panicking, you can also use Result enum.
``` rust
#[cfg(test)]
mod tests {
	fn it_works() -> Result<(), String> {
		if test_function(x, y) == expected_value {
			Ok(())
		} else {
			Err(String::from("Stuff went wrong here"))
		}
	}
}
```

---
Categories: [[Rust]], [[Debug]]
References:
Created: 2024-05-14
