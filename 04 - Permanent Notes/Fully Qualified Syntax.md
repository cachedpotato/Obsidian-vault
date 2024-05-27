---
tags:
---
# Fully Qualified Syntax
There are no boundaries to how traits are implemented (unless you get compiler errors of course), meaning you can implement multiple types with identically named methods to a type:

``` rust
struct Reimu;
impl Reimu {
	fn fly(&self) {
		println!("what incident is it this time");
	}
}
trait Miko {
	fn fly(&self);
}
trait Human {
	fn fly(&self) {
		println!("*flailing arms*");
	}
}
impl Miko for Reimu {
	fn fly(&self) {
		println!("*floats effortlessly*");
	}
} 

fn main() {
	let reimu:Reimu = Reimu;
	reimu.fly();
}
```
`Reimu` has three different methods with the same name, and in the code we called the `fly()` method without specifying anything. Question is: which method will be called?
```
cargo run
what incident is it this time
```
We can see that Rust prioritizes direct implementations on the type first, instead of traits. To use trait methods, we need to specify as the following:
``` rust
fn main() {
	//trait::method(&param)
	Miko::fly(&reimu);
	Human::fly(&reimu);
}
```

## Associated Functions and ambiguity
Unlike methods, Associated functions do not have the `self` parameter. If similar situation as above happened for associated functions, would there be additional problems?
```rust
struct Dog;
impl Dog {
	fn name() -> String {
		String::from("doggo")
	}
}
trait Animal {
	fn name() -> String;
}
impl Animal for Dog {
	fn name() -> String {
		String::from("Doge")
	}
}

fn main() {
	let dog = Dog;
	println!("{}", Dog::name());
	println!("{}", Animal::name()); //raises error
}
```
Because the examples above do not have any parameters, problems arise when we try to call the `name()` function for the `Animal` trait. We get an error saying:
```
$ cargo run
   Compiling traits-example v0.1.0 (file:///projects/traits-example)
error[E0790]: cannot call associated function on trait without specifying the corresponding `impl` type
  --> src/main.rs:20:43
   |
2  |     fn name() -> String;
   |     ------------------------- `Animal::name` defined here
...
20 |     println!("{}", Animal::name());
   |                                           ^^^^^^^^^^^^^^^^^ cannot call associated function of trait
   |
help: use the fully-qualified path to the only available implementation
   |
20 |     println!("{}", <Dog as Animal>::name());
   |                                           +++++++       +

For more information about this error, try `rustc --explain E0790`.
error: could not compile `traits-example` (bin "traits-example") due to 1 previous error
```
Because `Animal` trait can be implemented by any type, Rust does not know which implementation to use, thereby raising a compiler error. Thankfully, Rust compiler tells us the solution to this problem, we can simply use the `<Dog as Animal>::name()` for disambiguation. This is what's called a _fully qualified syntax_. Fully qualified syntax leaves no room for ambiguity, and it can be summarized as so:

```rust
<Type as Trait>::function(receiver_if_method, next_arg,...)
```
The receiver in this case refers to `self` and/or its references, which exist only in methods. 



---
Categories: [[Advanced Traits]]
References:
Created: 2024-05-27
