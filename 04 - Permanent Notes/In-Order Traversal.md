# In-Order Traversal
This algorithm will:
- start from the left-most leaf node
- move up to parent
- go straight down to the right
- Rinse and repeat
![[Pasted image 20240619185140.png|500]]
The reason this is called in-order is because if This is done in the context of a [[Binary Search Tree]], and create a list of traveled nodes in order, the list will always be sorted (I think).

Here is the code implementation in Python:
```python
from typing import Optional

class TreeNode
def inOrderTraversal(root: Optional[TreeNode]) -> List[int]:
	res = []
	def DFS(node: Optional[TreeNode]):
		if not node:
			return

		DFS(node.left)
		res.append(node.val)
		DFS(nod.right)

	DFS(root)
	return res
```

Here's a bonus Why not use Iterative approach?
```python
def inOrderTraversal(root: Optiona[TreeNode]) -> List[int]:
	if not root: return []
	stack = []
	curr = root

	res = []
	while stack and curr:
		while curr:
			stack.append(curr)
			curr = curr.left

		curr = stack.pop()
		res.append(curr.val)
		if curr.right:
			curr = curr.right
	
	return res
```

---
Categories: [[Traversal Algorithms]], [[Computer Algorithms]]
References:
