---
tags:
---
# Topological Sort
Topological sort is a sorting (or rather a traversal algorithm) for directed graphs. Because of the way graphs work, topological sort can have multiple outputs for the same graph depending on the algorithm.
![[Pasted image 20240710183021.png]]

## Base Idea
Here are the steps for topological sort
1) From an arbitrary starting point, use [[Depth First Search Algorithm|DFS]] to traverse through graph
2) If we reach an end point (no more nodes to traverse), we mark that node as visited, and add to path
3) Repeat the process until we've traversed the entire graph
4) Since the path list starts from the end, reverse the list and return

## Code
The example code below assumes edges will be given in `[v1, v2]` form of vertex pairs.

```python
def topologicalSort(n: int, edges: List[List[int]]) -> List[int]:
	#n is the number of vertices in graph
	nodes = {i: [] for i in range(n)}
	for curr, prev in edges:
		nodes[curr].append(prev)


	result = []
	visited = set()
	cycle = set()

	def dfs(v: int):
		if v in visited or cycle:
			return
			
		#added functionality for loop checking
		cycle.add(v)
		for next in edges[v]:
			dfs(v)
				
		cycle.remove(v)
		visited.add(v)
		result.append(v)


	for i in range(n):
		dfs(i)

	#currently the result list starts from the end
	#flip it and return
	result.reverse()
	return result
```

## Traversing Undirected Graph
unlike directed graph, where there is a clear order of nodes, undirected graph does not have a set order of nodes. To traverse all nodes within an undirected graph, we need to make slight adjustments to the code above.

below is a code for checking if we have multiple unconnected graphs (or multiple connected components)
```python
def traversUndirectedGraph(n: int, edges: List[List[int]]) -> bool:
	nodeMap = {i: [] for i in range(n)}
	visited = [False] * n
	for v1, v2 in edges:
		nodeMap[v1].append(v2) 
		nodeMap[v2].append(v1)


	def dfs(curr, prev):
		if visited[curr]:
			return
		visited[curr] = True
		for v in nodeMap[curr]:
			#case 1: curr -> v (prev) && v(prev) -> curr
			#skip this infinite loop
			if v == prev:
				continue
			dfs(v, curr) #current becomes previous


	#starting point does not matter - one dfs will traverse
	#through the entire connected graph
	#set initial previous to -1
	dfs(0, -1)
	for v in visited:
		if not v: return False
	return True
```


---
Categories: [[Graphs]], [[Computer Algorithms]]
References:
