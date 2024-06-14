---
tags:
---
# Sorting Algorithms
There are a LOT of algorithms when it comes to sorting arrays. Here are some of the more popular and the most important sorting algorithms.

1) Selection Sort: `O(n^2)` algorithm.
Pseudocode:
```
for i in [0, n - 2]:
	for j in [i + 1, n - 1]:
		get the minimum value of the array
	replace array[i] with said minimum value
quit
```
Implementation:
```C++
void selection_sort(int nums[]) {
	for (int i = 0; i < len(nums) - 1; i++ ) {
		for(int j = i; j < len(nums); j++) {
			if (nums[j] < min) {
				min = nums[j];
				idx = j;
			}
		}
		int temp = nums[i];
		nums[i] = min;
		nums[idx] = temp;
	}
}
```

2) Bubble Sort: `O(n^2)` algorithm
Pseudocode:
```
repeat n - 1 times
for i in [0, n - 2]:
	if array[i] > array[i + 1]:
		swap

if no swap:
	quit
```
Implementation:
```C++
void bubble_sort(int nums[]) {
	int swap;
	int n = len(nums);
	while (n > 0) {
		swap = 0;
		for (int i = 0; i < len(nums) - 2; i++) {
			if nums[i] > nums[i + 1] {
				int temp = nums[i + 1];
				nums[i + 1] = nums[i];
				nums[i] = temp;

				swap = 1;
			} 
		}
		if (swap == 0) {return;}
		n -= 1;
	}
}
```
4) [[Merge Sort]]: `O(nlogn)` algorithm.
5) [[Quicksort]]: The fastest sorting algorithm.

---
Categories: [[Computer Algorithms]], [[CS50 - Introduction]]
References:
Created: 2024-06-13
