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


---
Categories: [[Rust]]
References:
Created: 2024-05-16
