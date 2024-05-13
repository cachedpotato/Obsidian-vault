---
tags:
  - Rust
---
# Hash Map in Rust
Hash map, compared to other collections, used less and lacks macro support for creating one, let alone not being included in the prelude. Still Hash maps are very useful. O(1) enjoyers anyone?
```rust
use std::collections::HashMap
let mut map: HashMap<String, u32> = HashMap::new();
```
HashMap data is stored in (key, value) pairs. 
To insert values, simply use the ```insert``` function.
```rust
map.insert("Blue".to_string(), 10);
map.insert("Violet".to_string(), 20);

println!("map: {:?}", map); //HashMap has Debug trait
```

## Accessing values in hash map
Remember how in vectors the ```get``` method returned an Option instead of the actual value for safety measures? the same thing applies in hash map. However, we need to go through a few more steps:
```rust
let key: String = String::from("red");
let val: u32 = map.get(key) //returns Option(&u32)
	.copied() //returns Option(u32)
	.unwrap_or(0); //returns u32

println!("Red team score: {val}, but red does not exist");
```
because we used ```get``` with ```unwrap_or```, upon lookup failure the code will return whatever we put in the latter function rather than panicking. In conclusion, to get a value:
- ```map.get(key).copied().unwrap_or(errcond)```

## Iterating in HashMap
just like vector iteration, we want to pass the reference of the map for looping so that the loop does not gain ownership. We also need to dereference the values first to make any changes
```rust
for (k, v) in &map {
	println!("{k}: {v}"); //or just use {:?} for debug style printing
}
```

## Updating hash map values
there are 3 major ways of updating values

### Overwriting

```rust
map.insert(String::from("Violet"), 30); //violet value changed from 20 to 30
```
Once overwritten we won't be able to get the previous value back.

### ```or_insert()```

```rust
map.entry("red")
	.insert_or(5);
```
- entry() gives ```Entry<_, K, V>``` type.
- ```insert_or(v)``` either updates/overwrites previous value if the key is an existing one, or creates a new pair if the given key does not yet exist in the hash map.

### updating values based on previous values

```rust
use std::collections::HashMap;

let string: String = String::from("silent night beautiful night");
let mut word_count: HashMap<String, u32> = HashMap::new();
for word in string.split_whitespace() {
	//if the key exists, get the value. If not, add a new node with count 0
	let count: u32 = map.entry(word).or_insert(0)
	*count += 1; //dereferencing first

println!("map: {:?}")
//{"beautiful" : 1, "night": 2, "silent": 1}
}
```


---
Categories: [[Rust]], [[Data Types]]
References:
Created: 2024-05-12