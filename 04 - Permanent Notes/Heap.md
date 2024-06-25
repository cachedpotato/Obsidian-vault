---
tags:
---
# Heap
Heap is a data structure where the values are _somewhat_ sorted. This may sound a little vague, so to specify, Heaps are generally divided into two types:
- Min Heap: Stores k smallest values
- Max Heap: Stores k largest values
The reason heap is somewhat sorted is because of it's unique property between child nodes and parent nodes. For the case of min heap, the parent node is always going to be _SMALLER_ than its child, whereas the max heap the parent will be _BIGGER_. This way, some level of order is maintained, with the root node being either the largest (for the case of max heap) or the smallest (for the case of min heap).

## Difference from [[Binary Search Tree]]
The general structure of heap is similar to a binary tree, but there's one key difference: Heap has no distinction between left and right child nodes. Binary Search Tree, in this sense, is a lot stricter than heap, because not only does it have to maintain the `left child < parent < right child` rule, this has to be applied to _ALL POSSIBLE SUBTREES_, whereas heap just need to make sure the child is smaller/bigger than parent.

## Implementations
Because heap structure is used ubiquitously, We don't need to create heap from scratch. For example in python we already have the `heapq` module:
```python
from collections import heapq
myMinHeap = [1, 2, 3, 3, 5, 5, 5]
heapq.heapify(myMinHeap)
heapq.heappop(3)
heapq.heappush(5)

print("Easy Peasy")
```

## Making heap from scratch
If we do need to create heap structure ourselves, Here's the basic plan for "heapifying" an array. We are going to do two things:

- Use the fact that a child node for a parent node of index `i` are `2*i + 1` and `2*i + 2 .
- Starting from the innermost parent node (`2*n + 1`)Recursively swap call the `heapify` function to swap values up/down so that we get a full min/max heap, like so:
![[Pasted image 20240624153726.png|500]]
Here's an implementation in C++:
```c++
#include <vector>
class maxHeap {
public:
	void swap(int *i, int *j) {
		int temp = i;
		*i = *j;
		*j = temp;
	}

	void heapify(std::vector<int>& heap, int i) {
		int size = heap.size();
		int largest = i;
		int l = 2*i + 1; //left child
		int r = 2*i + 2; //right child

		if (l < size && heap[i] < heap[l]) {
			largest = l;
		}

		if (r < size && heap[i] < heap[r]) {
			largest = r;
		}

		if (i != largest) {
			maxHeap::swap(&heap[i], &heap[largest]);
			maxHeap::heapify(heap, largest)
		}
	}

	void heap_insert(std::vector<int>& heap, int n) {
		if (heap.size() == 0) {
			heap.push_back(n);
			return;
		}
		
		heap.push_back(n);
		int size = heap.size();
		for (int i = size/2 - 1; i >= 0; i--) {
			maxHeap::heapify(heap, i);
		}
	}

};
```

---
Categories: [[Data Structure]], [[Memory Management]]
References:
