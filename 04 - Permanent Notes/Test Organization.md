---
tags:
---
# Test Organization
The rust community things about tests in terms of two main categories: unit test and integration test.

## Unit test
Small tests. Test one module at a time. Can test private interfaces.
the ```cfg``` in ```#[cfg(test)]``` stands for configuration, and tells Rust that it should only be included given a certain configuration option, in this case test.

As mentioned above, you can test private functions as well.
``` rust
pub fn add_two(a: i32) -> i32 {
    internal_adder(a, 2)
}

fn internal_adder(a: i32, b: i32) -> i32 {
    a + b
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn internal() {
        assert_eq!(4, internal_adder(2, 2));
    }
}
```
the ```internal_adder``` function is not public, but we brought them and its parents into scope using the ```use super::*``` command. 

## Integration Test
_ENTIRELY EXTERNAL_ to your library. Use only public interface. Test multiple modules at once, to see if many parts of your entire library works correctly.
to do integration test, you first need to make a tests directory.
each file in tests is a different crate, so you need to bring stuff into scope manually.
``` rust
//tests/integration_test.rs
use adder;
#[test]
fn it_adds_two() {
	assert_eq!(adder::add_two(2), 4);
}
```
Unlike unit tests, you do NOT annotate with ```#[cfg(test)]```. this is because cargo treats the tests directory specially and compiles files in the directory only when you're running ```cargo test```, which is EXACTLY what the annotation is meant to do.

### submodules in integration tests
as your project grows, your tests will grow as well, and at some point you might want to use modules exclusively for testing for convenience purposes. However, since the entirely of tests directory is treated as a testing function, whatever function is declared there, ```cargo test``` will run it as a test. To avoid this, you can use the _old naming convention for modules_:

```
├── Cargo.lock
├── Cargo.toml
├── src
│   └── lib.rs
└── tests
    ├── common
    │   └── mod.rs
    └── integration_test.rs

```
by old conventions, we mean the .../module_name/mod.rs. after this, in the integration test file, we simply add the module:
``` rust
use adder; //our crate
mod common; //module name
```

---
Categories: [[011-Rust]], [[Debug]], [[Testing in Rust]]
References:
Created: 2024-05-14
