---
tags:
---
# Breadth First Search Algorithm
Breadth First Search, or BFS for short, is a tree-searching algorithm that searches _LEVEL BY LEVEL, HIGHEST TO LOWEST_.

![[Pasted image 20240619184806.png]]

BFS uses queues, because it needs to pop whatever was put FIRST. In other words, BFS uses FIFO data structures.

## Pseudocode
```
function BFS:
	if root empty: return Null

	queue.add(root)
	while queue != empty:
		for _ in range(length(queue)):
		
			currentNode = q.pop()
			process(currentNode)
			
			if currentNode.left exist:
				q.add(currentNode.left)
			if currentNode.right exist:
				q.add(currentNode.right)
				
```
## Code Example - Level order Traversal
```python
from typing import Optional
from collection import deque

class TreeNode:
	def __init__(self, val:int = 0, left:TreeNode = None, right:TreeNode = None):
		self.val = val
		self.left = left
		self.right = right

def BFS(root: Optional[TreeNode]) -> List[List[TreeNode]]
	if not root:
		return []

	res = []
	q = deque()
	q.append(root) 
	while q:
		level = []
		for _ in range(len(q)):
			
			curr = q.popleft()
			level.append(q)

			if q.left:
				q.append(q.left)
			if q.right:
				q.append(q.right)

		res.append(level)
	return res
```


---
Categories: [[Computer Algorithms]]
References:
