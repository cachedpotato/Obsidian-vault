---
tags:
---
# Floyd's Algorithm
Suppose we are given a linked list with exactly ONE cycle. we are not given the information on where it starts, how big it is, but we know that one cycle exists, and the head of the linked list is NOT in the cycle. How do we figure out the node where the cycle starts? This is where Floyd's algorithms comes in.

## The Concept
Floyd's algorithm has two phases:

- Phase 1) using the fast and slow pointer method, find the node where the two intersect.

- Phase 2) have another pointer set to the head of the list. move both pointers until they meet. the intersection node is _GUARANTEED_ to be the starting point of the cycle

Why are we guaranteed to find the starting point this way?
![[Pasted image 20240613104406.png]]
suppose the intersection at phase 1 happened at the intersection node annotated in the above figure. the let the distance between the starting point and the start of the cycle p, and the distance between the intersection and the start of the cycle x. let the length of the cycle be c.

Because of how fast and slow pointers work, the intersection will have happened after fast pointer have moved exactly two times the distance slow pointer traveled:
$$
2d(slow) = d(fast)
$$
using the numbers and labels given above:
$$
2(p + c - x) = (p + 2c - x)
$$
$$
\therefore p  =  x
$$

## Writing the actual algorithm
While the concept isn't so intuitive, thankfully the code implementation is dead simple:
```python
def floyd_algorithm(head: Node) -> Node:
	#phase 1
	slow = fast = head
	while True:
		slow = slow.next
		fast = fast.next.next
		if slow == fast:
			break

	#phase 2
	slow2 = head
	while True:
		slow = slow.next
		slow2 = slow2.next
		if slow == slow2:
			return slow
```

## Usage
This is also used for finding duplicates within a length n + 1 list, where the possible values are in [1, n] inclusive, and there is only ONE duplicate.

| 0   | 1   | 2   | 3   | 4   |
| --- | --- | --- | --- | --- |
| 1   | 2   | 3   | 2   | 2   |
Say we are given the list above. the index is the first row, and the second row contains the values. While we can solve this trivially either by sorting or using a hash map, there exists a way to solve this using only O(1) additional space, and that is Floyd's algorithm. Because the values are in [1, n], we can think of the list as a linked list, where the values hold the node pointer. For example. node 0 points to 1, and node 2 points to itself, etc. 

![[Pasted image 20240613111729.png]]

Because there is only one duplicate, this means only one node has multiple pointers pointing towards itself, which creates a cycle. Using this fact, we can use the Floyd's algorithm to find the starting point of the cycle, which in this case is the duplicate number. Node hopping will be done by the `[]` "operation".

``` python
def find_duplicate(nums: List) -> int:
	#floyd's algorithm
	slow = fast = 0
	while True:
		slow = nums[slow]
		fast = nums[nums[fast]]
		if slow == fast: breakA

	slow2 = 0
	while True:
		slow = nums[slow]
		slow2 = nums[slow2]
		if slow == slow2: return slow
```

---
Categories: [[Computer Algorithms]]
References:
Created: 2024-06-13
