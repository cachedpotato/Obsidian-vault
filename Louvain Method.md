---
tags:
---
# Louvain Clustering
Louvain Clustering, in its simplest form, is a hierarchical clustering mechanism on a network that reduces a cluster into one node on each pass (iteration).

Louvain method uses a greedy optimization algorithm which aims to optimize the [[Modularity (Network Science)|modularity]], which has the big O of $O(n*logn)$ where $n$ is the number of nodes. It will iteratively optimize until no further significant increase in modularity is detected or a set number of iteration has been reached.

## The Algorithm
Louvain method can be divided into two phases: Modularity optimization and community aggregation.
![[louvain-modularity-algorithm-2.png|500]]
### Modularity Optimization
Given a network of N nodes, we first assign a different community to each node of the network. Then for each node $i$ we consider the neighbors of $i$ $j$, and we evaluate the change in modularity we would get by removing $i$ from its community and _moving_ it to community of $j$. $i$ is placed in the community for which this gain is the positive maximum. This is done to all nodes until no further improvements is achieved.

given modularity of
$$
Q = \frac{1}{2m}\sum_{i,j}\left[ A_{ij}-\frac{k_{i}k_{j}}{2m} \right]\delta (c_{i}, c_{j}),
$$
Louvain calculates the gain in modularity $\Delta Q$ by the following:
$$
\Delta Q = \left[ \frac{\sum_{in}+2k_{i,in}}{2m} - \left( \frac{\sum_{tot}+k_{i}}{2m} \right)^2\right] - \left[ \frac{\sum_{in}}{2m}-\left( \frac{\sum_{tot}}{2m} \right)^2 - \left( \frac{k_{i}}{2m} \right)^2 \right]
$$
Where 
- $\sum_{in}$ is the sum of the weights of the links inside C
- $\sum_{tot}$ is the sum of the weights of the links incident to nodes in C
- $k_i$ is the sum of the weights of the links incident to node i
- $k_{i,in}$ is the sum of the weights of the links from i to nodes in C 
- $m$ is the sum of the weights of all the links in the network.

### Aggregation of community
In this phase, we build a new network in which each nodes are the community defined in the previous phase.
The weights of the links between nodes are given by the sum of the weight of the links between nodes in the corresponding two communities. Links within the community will appear as self loops.

We can repeat these two phases until no further increase in modularity is achieved, or after a set number of passes has been reached.

---
Categories: [[Clustering]], [[Community Detection]]
References:
https://iopscience.iop.org/article/10.1088/1742-5468/2008/10/P10008
https://neo4j.com/blog/graph-algorithms-neo4j-louvain-modularity/
https://www.nature.com/articles/s41598-019-41695-z
https://en.wikipedia.org/wiki/Louvain_method

Created: 2024-05-22
