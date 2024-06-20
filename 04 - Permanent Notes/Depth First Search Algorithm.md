---
tags:
---
# Depth First Search Algorithm
Depth First Search, or DFS for short, is a tree-searching algorithm that searches _FROM THE LOWEST LEVEL TO HIGHEST LEVEL_.
![[Pasted image 20240619185140.png|500]]

Because DFS goes straight to the bottom level first, then goes up and down again, it uses data structure that has the LAST IN FIRST OUT properties. In other words, DFS uses stacks.

While both [[Breadth First Search Algorithm|BFS]] and DFS can use recursive method, generally BFS uses iterative approach and DFS uses recursive approach. Here, we'll see BOTH iterative method and recursive method for DFS

## Pseudocode
```
function DFS:
	if root empty: return Null

	current = root
	stack = []
	while current is not Null or stack is not Null:
		while current is not Null:
			stack.add(current)
			current = current.left

		current = stack.pop()
		process(current)

		current = current.right
```

## Code Example - In-Order Traversal (Iterative)
``` python
from typing import Optional

class TreeNode:
	def __init__(self, val:int = 0, left:TreeNode = None, right:TreeNode = None):
		self.val = val
		self.left = left
		self.right = right

def DFS(root: Optional[TreeNode]) -> List[List[TreeNode]]:
	if not root: return []
	res = []

	stack = []
	curr = root
	while stack or curr:
		while curr:
			stack.append(curr)
			curr = curr.left

		curr = stack.pop()
		res.append(curr)

		if curr.right:
			curr = curr.right

	return res
```

## Code Example - In-Order Traversal (Recursive)
```python
def Wrapper(root: Optional[TreeNode]):
	res = [] 
	def DFS(root: Optional[TreeNode]):
		if not root:
			return
		if root.left:
			DFS(root.left)
		if not root.left and not root.right:
			res.append(root)
			return
		if root.right:
			DFS(root.right)

	DFS(root)
	return res
```

## Code Example: Maximum-Depth (Recursive)
```python
def maxDepth(root: Optional[TreeNode]) -> int:
	if not root: return 0
	return 1 + max(maxDepth(root.left), maxDepth(root.right))
```


---
Categories: [[Computer Algorithms]]
References:
