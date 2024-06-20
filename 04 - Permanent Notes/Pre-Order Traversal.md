---
tags:
---
# Pre-Order Traversal
Unlike In-Order Traversal or Post-Order Traversal, Pre-Order Traversal starts from the root, then iteratively goes from left to right.
![[Pasted image 20240619201020.png|500]]

## The Code
```python
def Wrapper(root: Optional[TreeNode]) -> List[int]:
	res = []
	def preOrderTraversal(root: Optional[TreeNode]):
		if not root:
			return
		res.append(root.val)
		if root.left:
			preOrderTraversal(root.left)
		if root.right:
			preOrderTraversal(root.right)

	preOrderTraversal(root)
			
	return res
```


---
Categories: [[Traversal Algorithms]]
References:
