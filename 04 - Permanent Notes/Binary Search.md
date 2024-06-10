---
tags:
---
# Binary Search
Searching for a given target in a list takes `O(n)` time. However, we can get this down to `O(logn)` if we use the Binary Search (unfortunately abbreviated into BS) algorithm.

## Basic Thought Process
We are given a sorted list. how do we figure out where the target value is located? Because this list is sorted, we can do the following:
1) Split the list into 2 equal parts
2) Record the index of the split
3) If the target is bigger than the split, we look at only the upper half of the list
4) If the target is smaller than the split, we need look only the lower half of the list
5) Repeat the splitting process until we get the solution

Because we are looking at half of the previous size of the sub-list, the total computation time goes all the way down to `O(logn)`!

## Edge case - both pointers at the same index
because we will be using a while loop until the pointers cross, the question becomes: what do we do when both pointers are at the same position? Take a list of 1 element for example.
```rust
let list: [i32;1] = [1];
let l = 0
let r = len(list) - 1 // == l!

//uhh what do we do in this case?
//while l < r? while l <= r?
```
While pointers `l` and `r` are at the same position, the `while` loop hasn't evaluated yet. after evaluation, either 1) the pointers will cross and break out of the loop or 2) it is the value we want and we return the value. In conclusion, we should be using `while l <= r`.

## The code
Here's the actual code written in Rust.
``` rust
fn binary_search(target: i32, list: Vec<i32>) -> Result<i32, String> {
	let l: usize = 0; //leftmost index
	let r: usize = list.len() - 1; //rightmost index
	while l <= r {
		//not using (r + 1)/2 to avoid overflow issue
		split: usize = l + (r - l) / 2;
		if list[split] < target {
			//index of target is smaller than split
			r = split - 1;
		} else if list[split] > target {
			//index of target is bigger than split
			l = split + 1;
		} else {
			return Ok(split)
		}
	}

	Err("Target not in list".into()) //not found
}

fn main() {
	let list: [i32; 5] = [0, 1, 3, 10, 21];
	let target: i32 = 10;
	let res: i32 = binary_search(target, list).unwrap();
	println!("target is at index: {}", res);
}
```

---
Categories: [[Computer Algorithms]]
References:
Created: 2024-06-10
