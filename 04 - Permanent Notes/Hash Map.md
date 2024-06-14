---
tags:
---
# Hash Map
Hash map can be thought of as a collection of (key, value) pairs. key can be anything that can be indexed (which varies from language to language) and values are the data we want to actually store. The "key" of hash maps (pun 100% intended) is that we can search the value we desire with the key portion of the pair, and this can be done in **O(1) TIME**. When it comes to search time complexity, there's little to none that is as efficient as hash maps.

## Structure and Hash Function
Hash functions are what makes this all possible. We enter a key, the key undergoes some changes with the hash function, and we point to whatever that function returns, which contains the address of the stored data. Therefore, Hash Map can be summarized into this one picture:
![[Pasted image 20240610104220.png]]
Depending on the use case, having multiple values in the same index can be desired or can be an artefact of something known as conflict, where the hash function erroneously maps different keys to the same value.

## When to use Hash Maps?
Umm... **Anywhere?**. Hash map's O(1) search time is EXTREMELY powerful, and is used in a very wide variety of situations. Hash Maps can be extra helpful for things such as:
1) Storing count data: track how many times the key appears in a list
2) Data where searching is the primary focus (fast lookup time required)

Of course, hash maps are not without its drawbacks - it's relatively big in size, and most of all, hash maps must be stored in the heap, which means while yes the searching is O(1), it is still slower than searching inside the memory stack. If your data will keep changing size and/or is big, consider using hash maps. If not, then fixed-size arrays can be sufficient.

### Hash maps as a means of linked list management
when it comes to [[Linked List|linked lists]], because of it's complexity with pointers sometimes it's better to have a separate hash map with key: Node pairs. This way, we can manage and rearrange linked lists a lot faster, at the cost of O(n) additional space.
The basic workflow is like this 
1) create a hash map with key: Node pairs, initialize pointers to be `None`
2) Access nodes through hash and connect them as needed

ex) deep clone of linked lists
1) Have a hash map of Key(original node): Node(new node) pair
2) connect nodes just like how the original list is connected through hash lookup
``` python
#--snip
def deep_clone(head: Optional[Node]) -> Optional[Node]:
	dummy = head
	node_pairs = {}
	deep_clone = Node()
	while dummy:
		new_node = Node(dummy.val)
		node_pairs[dummy] = new_node
		dummy = dummy.next

	#connection
	dummy2 = head
	while dummy2:
		node_pairs[dummy2].next = node_pairs[dummy2.next]
		dummy2 = dummy2.next

	return node_pairs[head]
```

ex2)[[LRU cache]], or doubly linked list management
As is the case of LRU cache, there are times where we need to completely rearrange the order of doubly linked list. Using hash maps, we can instantly look up where it needs to be located and reconnect the list accordingly. Details are shown in the LRU cache note.

---
Categories: [[Data Structure]]
References:
Created: 2024-06-10
