---
tags:
---
# Controlling Tests in Rust

## Parallelism
Rust's ```cargo test``` runs tests in a parallel fashion. Because of this, we should be careful with tests that may depend on each other or use the same data, for example an external text file. It's cases like these where parallelism isn't preferred. In such cases, use the ```test-threads``` flag.
```
cargo test -- --test-threads=1
```

## Showing function output
By default, Rust's test library captures anything printed to stdout upon success. This means that for success cases we don't see what's actually being printed. To see this, use the ```show output``` flag.
```
cargo test -- --show-output
```

## Running subset of tests by name
consider the case where we have multiple tests, but only want to run a few of them:
``` rust
pub fn add_two(a: i32) -> i32 {
    a + 2
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn add_two_and_two() {
        assert_eq!(4, add_two(2));
    }

    #[test]
    fn add_three_and_two() {
        assert_eq!(5, add_two(3));
    }

    #[test]
    fn one_hundred() {
        assert_eq!(102, add_two(100));
    }
}
```

running ```cargo test``` will test all three cases. But what if we want to run only ```one_hundred()```? we can do so by specifying the name of the test.
```
cargo test one_hundred
```

We can also use parts of the test functions' name to run tests that has that part in its name, kind of like grep:
```
cargo test add
```

This will run both ```add_one_and_two``` ```add_three_and_two``` but not ```one_hundred```. 

## Ignoring tests
There are tests where you don't want to run every single time you do testing. In this case, add the ignore attribute.

``` rust
#[test]
fn this_test_runs() {
	assert!(test_function(x) == expected_output);
}

#[test]
#[ignore]
fn this_test_is_ignored() {
	assert!(test_function_2(x, y) == expected_output_2);
}
```
upon ```cargo test```, only ```this_test_runs``` will be tests. some notes about ignore:
- if you want to run only the ignored tests:
	- ```cargo test -- --ignored```
- if you want to include ignored tests:
	- ```cargo test -- --include-ignored```


---
Categories: [[Rust]], [[Debug]], [[Testing in Rust]] 
References:
Created: 2024-05-14
