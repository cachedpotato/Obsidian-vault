---
tags:
---
# Test Driven Development
With binary and library crates separated, we can test functions without needing to call the main function. This will become useful for Test Driven Development (TDD)

TDD is a development process with following steps:
- Write a test that should fail at first.
- Write or modify code to make the new test pass
- [[Refactoring|refactor]] code to make sure tests continue to pass

Essentially, write the tests fist as the blueprint for what we want to achieve, then go from there, instead of other way around.

For example, we want to make a search function that gives us a list of lines that contain a certain word. First, we make a test function like so:
```rust
#[cfg(test)]
mod tests {
	use super::*;
	#[test]
	fn one_result() {
		let query = "Duct"
		let contents = "\
Ductapes are cool.
ductpipe.
what am I doing with my life?";
		assert_eq!(search(&query, &contents), vec!["Ductapes are cool."])
	}
}
```
At first this won't even compile because we don't even have the ```search``` function yet. let's add that.

```rust
fn search<'a> (query: &'a str, contents: &'a str) -> Vec<&'a str> {
	vec![] 
}
```
Note that we added the _BARE MINIMUM_ of what we need to compile. running ```cargo test``` will still result in failed test, but at least it will succeed to compile. One step at a time.

Next, the actual body of the search function.
```rust
fn search<'a> (query: &'a str, contents: &'a str) -> Vec<&'a str> {
	let mut out: Vec<&str> = vec![];
	for line in contents.lines() {
		if line.contains(query) {out.push(line);}
	}
	out
}
```
Now the test will succeed. Yay!

The takeaway here is that 1) you make the TEST first then 2) one step at a time, build the function that passes the test.

---
Categories: [[Programming]]
References:
Created: 2024-05-15