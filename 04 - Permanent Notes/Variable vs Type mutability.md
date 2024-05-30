---
tags:
---
# Variable vs Type mutability
Remember how in iterations we once had to dereference something?:

``` rust
use std::collections::HashMap;
let text = "hello world!";

let mut map: HashMap<&str, i32> = HashMap::new();
for word in text.split_whitespace() {
	let count = map.entry(word).or_insert(0);
	*count += 1; //this right here
}
println!("{:?}", map);
```
a ```or_insert```'s definition is the following:
``` rust
pub fn or_insert(self, default: V) -> &'a mut V;
```
we can see that it returns a mutable reference. However, ```count``` itself is not mutable. Therefore, _THIS IS AN IMMUTABLE REFERENCE TO A MUTABLE VALUE_.

Now consider this example:
``` rust
pub fn build<T>(mut args: T) -> Result<T, &'static str>
where
	T: Iterator<Item = String>, {}
```
we can see the ```mut``` is in the _VARIABLE_ side of the argument, _NOT THE TYPE (T)_. this means that ```args``` _ITSELF IS MUTABLE_. This is the same as your run of the mill declaration of variables: 

``` rust
let mut args: i32 = 9; //args is mutable
args = 3; //this is possible

let args: &mut 3; //args is immutable.
args = &2; //This WONT COMPILE
*args = 2; //THIS WILL
```

The difference between the last two lines is that one is trying to change args itself, which is immutable, and one is trying to change the value args is referencing to. This is why we have to dereference (\*) it first.

## Moral of the story?
``` rust
let mut args = &3;
let args = &mut 3;
```
...These 2 are different. One means the variable itself can be mutated, and the other means the value the variable is referencing to is mutable. 

## Mutability in function parameters
say we have a function that _CONSUMES_ the vector it's given and returns a fresh new vector with additional element:
```rust
fn main() {
	let mut v: Vec<i32> = vec![0, 1, 2];
	let v1: Vec<i32> = add_three(v);
	assert_eq!(v1, vec![0,1,2,3]);
}

fn add_three(v: Vec<i32>) -> i32 {
	v.push(3);
	v
}
```
We set the vector `v` to be mutable, which is then passed into the function and is consumed, all is well... NOT! because we did not specify in the _function parameter_ that it's going to be borrowed as mutable!
```
warning: variable does not need to be mutable
  --> exercises/move_semantics/move_semantics3.rs:13:9
   |
13 |     let mut vec0 = vec![22, 44, 66];
   |         ----^^^^
   |         |
   |         help: remove this `mut`
   |
   = note: `#[warn(unused_mut)]` on by default

error[E0596]: cannot borrow `vec` as mutable, as it is not declared as mutable
  --> exercises/move_semantics/move_semantics3.rs:21:5
   |
21 |     vec.push(88);
   |     ^^^ cannot borrow as mutable
   |
help: consider changing this to be mutable
   |
20 | fn fill_vec(mut vec: Vec<i32>) -> Vec<i32> {
   |             +++

error: aborting due to 1 previous error; 1 warning emitted

For more information about this error, try `rustc --explain E0596`.
```
As the compiler kindly suggests, we need to specify `mut v: Vec<i32>` in the function signature as well!


---
Categories: [[Rust]]
References:
Created: 2024-05-16
