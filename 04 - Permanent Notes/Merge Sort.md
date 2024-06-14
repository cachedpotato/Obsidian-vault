---
tags:
  - NeedWork
---
# Merge Sort
Merge sort implements [[Recursion|recursive approach]] for sorting an array. it will split arrays into half, and sort that, then merge it all together. Visualizing the basic workflow would look something like this:
![[merge-sort-example_0-.1-1042020650.png | 500]]
## Pseudocode
Merge sort, as can be seen above, can be split into 2 phases.

1) PHASE 1 - DIVISION: Recursively split the array into equal halves. if the array is of size 1, it can't go any lower, and it's considered sorted.

2) PHASE 2 - MERGING: from the divided arrays, merge them back. because the subarrays will already be sorted when we are merging, we only need to look at the same index of each array for comparison.

the depth of this merge "tree", since we divide by half each time, will be of size `log2(n)`. each depth has `n` elements. Therefore, the time complexity will be `n * log2(n)`, so this is an `O(nlogn)` sorting algorithm.

## Implementation
As stated before, merge sort uses recursion, meaning it will call itself until it reaches the base case, then start merging. An example implementation in C++ would look something like this:
``` C++
void merge_sort(int nums[]) {
	//base case
		if (len(nums) == 1) {
			return;
		}

	//PHASE 1 - DIVISION
	int half_length = len(nums) / 2;
	int left[half_length] = nums[0:half_length];
	int right[len(nums) - half_length] = nums[half_length:len(nums)];

	//PHASE 2 - MERGING
	left = merge_sort[left];
	right = merge_sort[right];

	int merged[len(nums)];
	for(int i = 0; i < half_length; i++) {
		merged[i] = (left[i] < right[i]) ? left[i] : right[i];
		merged[i + 1] = (left[i] < right[i]) ? right[i] : left[i]; 
	}

	nums = merged;
}
```


---
Categories: [[Computer Algorithms]], [[Sorting Algorithms]], [[CS50 - Introduction]]
References:
https://www.worldofitech.com/merge-sort/
Created: 2024-06-13
