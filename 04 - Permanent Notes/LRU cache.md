---
tags:
---
# LRU cache
Cache is a space of memory that stores data that are looked up very often to speed up the looked up process. Cache is small be design, as having way too large cache size goes directly against the purpose of caching. Meaning, there will come a time where we have to update the cache and remove an item from the same time. Question is: what data do we remove?

The most intuitive answer is to remove the least recently used (LRU) data, and this is what most cache system does. Then the next question becomes: how do we know which data is least recently used?

The objective here is to
- have a cache with fixed memory size
- whenever we access/insert the data, it becomes the most recently used
- if the cache is full and we need to insert something, delete the least recently used data
- Searching and inserting must be done in `O(1)` time complexity.

## Basic Implementation
to have `O(1)` lookup time, we can use hash maps. But hash maps inherently does not store anything related to how recent the data was used. Using only the hash map isn't enough. What we need here, are the following:
1) a Doubly linked list of Nodes containing BOTH KEY AND VALUE
2) a `left` and a `right` pointer, each pointing to the least recently used and most recently used node, respectively
3) a hash map containing `key: NODE` _PAIRS, NOT KEY_VALUE_ (this will come in handy later). this means when we look up the hash, it will return the node containing both the key and the value.
![[Pasted image 20240613113330.png]]
Won't go into full details here, but this would be an implementation example using Python:
``` python
class Node:
	def __init__(self, key: int, val: int) -> None:
		self.key = key
		self.val = val
		self.next = None
		self.prev = None

class LRUCache:
	def __init__(self, capacity: int) -> None:
		self.cache = {}
		self.capacity = capacity

		#LRU, MRU pointer initialization
		self.left = Node(0, 0)
		self.right = Node(0, 0)
		self.left.next, self.right.prev = self.right, self.left

	#insert to the MOST RECENTLY USED side of the list
	def insert(self, node: Node) -> None:
		prv = self.right.prev
		prv.next = self.right.prev = node
		node.prev = prv
		node.next = self.right

	#remove node from list
	def remove(self, node: Node) -> None:
		prv, nxt = node.prev, node.next
		prv.next = nxt
		nxt.prev = prv

	def get(self, key: int) -> int:
		if key not in self.cache:
			return -1
		node = self.cache[key]
		self.remove(node)
		self.insert(node)
		return node.val
		
	def put(self, key: int, val: int) -> None:
		if key in self.cache:
			self.remove(node)
		self.cache[key] = Node(key, val)
		self.insert(self.cache[key])

		#if past capacity, remove lru node
		if len(self.cache) > self.capacity:
			lru = self.left.next
			del self.cache[lru.key]
			self.remove(lru)
```


---
Categories: [[Memory Management]]
References:
Created: 2024-06-13
