---
tags:
---
# Kadane's Algorithm
Kadane's Algorithm is a computer algorithm used to find the maximum sum subarray. It has a lot of overlaps with sliding windows and is the basis of most greedy algorithms.

## Maximum Subarray - O(n^2) Solution
First let's do this without the algorithm. The easiest (and the slowest) solution is to look at _all possible subarrays_ and get the result, like so:
```c++
int maximumSumSubarray(vector<int> array) {
	int out = array[0]; //init
	for (int i = 0; i < array.size(); i++) {
		//initialize subarray sum
		int curr = 0;
		for (int j = i; j < array.size(); j++) {\
			curr += array[j];
			out = max(out, curr);
		}
	}
	return out;
}
```
While this does work, as mentioned before this is a very slow algorithm - `O(n^2)` in fact - which is slower than sorting algorithms! How can we make it better?

## The Basis behind Kadane's Algorithm
There is one giant improvement that can be made with the previous algorithm with this simple thought process:

> Negative sums will only make our total sum smaller.

To elaborate: This is _NOT_ to say we shouldn't just skip negative values altogether. a small negative number can be followed by a giant positive number, greatly outweighing the effects of the negative number. The key word here is "effect". How do we know when the negative number is just too big? Of course, it would be when the total (current) sum becomes smaller than zero. Then, and only then, should we skip the negative number and move to a new starting point.

This is a greedy approach in the sense that we are only looking for cases that increases our current maximum sum. After the first initialization, the maximum sum will update in a strictly increasing fashion.

## Kadane's Algorithm - the Code
Enough talk, let's get into the code:
```C++
int KadanesAlgorithm (vector<int> array) {
	int maxSum = array[0];
	int currSum = 0;
	for (int &n: array) {
		//if currSum < 0 - reset
		currSum = max(currSum, 0);
		currSum += n;
		maxSum = max(maxSum, currSum);
	}
	return maxSum;
}
```
Iterating through the array _once_, we check
- if `currSum` is smaller than 0 - if so, reset the sum to 0
	- This part is the crux of this algorithm!
- update `currSum` by adding current value
- update `maxSum` by comparing previous `maxSum` with `currSum`

Because we're traversing through the array just once, this is an `O(n)` algorithm - much better than `O(n^2)`!

This code only tracks the maximum sum, what if we want to track the index as well?
```C++
pair<int, int> KadanesAlgorithmTwoPointer (vector<int> array) {
	int maxSum = array[0]
	int currSum = 0;
	int L = 0;
	int R = 0;
	pair<int, int> out = {L, R};

	for (int i = 0; i < array.size(); i++) {
		if (currSum < 0) {
			//reset - move L to where R is
			L = i;
			R = i;
			currSum = 0;
		}
		currSum += array[i];
		if (maxSum < currSum) {
			//update R
			R = i;
			maxSum = currSum;
		}
	}

	return out;
}
```




---
Categories: [[Computer Algorithms]], [[Greedy Algorithm]]
References:
