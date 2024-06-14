---
tags:
---
# Linked List
A linked list can be list of `Node`s, where each node stores:
- a value,
- pointer(s) that are linked to other nodes in the list
The most basic case of a linked list is a singly linked list, where there is only one pointer: `next`, that points to, well, the very next node.
![](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Ftse3.mm.bing.net%2Fth%3Fid%3DOIP.CLerHARLDMEdCWQE3n-o8AHaC9%26pid%3DApi&f=1&ipt=a429c44be830b1af743449262ca9d669e23bb36044eadece93f39604e18e1e3c&ipo=images)
This is a visualization of the aforementioned singly linked list. One thing to note is that the very end of the list will have the pointer point to `Null` (or `None`) depending on the language. The pointer that points to the very first node is often referred to as `head`, and the pointer that points to the very last node is referred to as `tail`.

There is also a doubly linked list, where there are two pointers: `prev` and `next`.
![[a627b7d78acee6ca68b96b940b58cf9b-2534097472.png|500]]

## When to use linked lists?
Singly linked lists are very basic, and can be thought of as the base idea of how lists are implemented in computer memory. more advanced linked lists such as doubly linked lists and cyclic linked lists, where the end node points to the very fist node, exist to add more functionality to base lists, such as accessing previous node. linked lists can also be thought of as a sequence, and also a precursor for [[Graphs]], where nodes are connected more freely.

## Reversing a singly linked list
reversing linked list is one of the most basic operations we can do, so it's better to just memorize how it works.
``` python
from typing import Optional
class Node:
	def __init__(self, val: int, next: Node): 
		self.val = val
		self.next = next

def reverse(head: Optional[Node]) -> Optional[Node]:
	prev, curr = None, head
	while curr:
		temp = curr.next #create a temp pointer to next node
		curr.next = prev #reconnect the current node to previous
		prev =  curr #current node now becomes the previous
		curr = temp #the next node becomes the current

	#repeat until we reach the final node
	#curr will be at None, and prev will point to the start of the reversed list
	return prev
```

## Algorithms used for linked list
- [[Fast and Slow Pointers]]: a "double pointer" approach used for linked lists. this can be used in a variety of ways, including:
	- figuring out whether the list has a cycle
	- finding out what node to delete (slow and fast will maintain a fixed size gap)

- [[Floyd's Algorithm]]: Used to figure out the starting point of a cycle when given a cyclic linked list

---
Categories: [[Data Structure]]
References:
Created: 2024-06-13
