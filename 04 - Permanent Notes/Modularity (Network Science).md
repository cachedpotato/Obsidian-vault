---
tags:
---
# Modularity (Network Science)
Modularity measures the strength of modules in a given network. In other words, it's a metric that shows how well a network has been partitioned in groups. Modularity takes a value between $\left[ -\frac{1}{2}, 1 \right]$ for weighted undirected graphs, and the higher the value, the well/stronger it's been partitioned.
![[modularity-graph-database-1.png|500]]

A formal definition of Modularity is the _fraction_ of the edges that fall within the given groups minus the expected fraction if edges were distributed at random. In other words:
$$
Modularity = \sum_{nodes}[(Adjacency) - (BaseNoise)]
$$

## Finding the Expected number of Edges
Let $A$ be the adjacency matrix of Network $G$ with $n$ nodes and $m$ links. Then, we can partition a graph into two such that a given node $v$, if it belongs to some community 1, its membership variable $s_{v} = 1$ and if not $s_v = -1$.

Let $k_v$ be node degree of $v$. Now, consider $k_v$ stubs (node + half the edge) of $v$. If there exists a connection between different stubs, say between $v$ and $w$, we can denote that as $I^{(v,w)} = 1$. if it does not exist, then $I^{(v,w)} = 0$. Then, the matrix $I$ can be seen as the "adjacency matrix" of stubs.

There are 2m stubs total in this Network. Therefore, the probability (naive approximation, or expectancy) of connection of a given stub with another stub in node w can be written as:
$$
p(I_{i}^{(v,w)} = 1) = E[I_{i}^{(v,w)}] =  \frac{k_{w}}{2m-1}
$$
Therefore, the expected number of full edges is:
$$
\begin{flalign}
E[J_{vw}] & = E\left[ \sum_{i=1}^{k_{v}}I_{i}^{(v,w)} \right] = \sum_{i=1}^{k_{v}}E[I_{i}^{(v,w)}] \\
& = \sum_{i=1}^{k_{v}} \frac{k_{w}}{2m-1} = \frac{k_{v}k_{w}}{2m - 1} \\
& \approx \frac{k_{v}k_{w}}{2m}
\end{flalign}
$$

## Modularity
Now that we know the expected number of full edges, we can calculate the actual modularity. The difference between actual number of edges and the expected number of it between node $v$ and $w$ is
$$
A_{vw} - \frac{k_{v}k_{w}}{2m}
$$
Summing over all nodes we finally get our modularity Q:
$$
Q = \frac{1}{2m}\sum_{v,w \in G}\left[ A_{vw} - \frac{k_{v}k_{w}}{2m} \right] \frac{s_{v}s_{w} + 1}{2}
$$
the $\frac{s_vs_w + 1}{2}$ will be 1 if $v$ and $w$ belong in the same partition, and 0 otherwise. rewriting this as $\delta(v,w)$, we get
$$
Q = \frac{1}{2m}\sum_{v,w \in G}\left[ A_{vw} - \frac{k_{v}k_{w}}{2m} \right] \delta (v,w)
$$
Alternatively, defining matrix $B$ such that $B_{vw} = A_{vw} - \frac{k_vk_w}{2m}$ and moving the 1/2 to the front gives:
$$
\begin{flalign}
Q & = \frac{1}{4m}\sum_{v,w \in G}\left[ A_{vw} - \frac{k_{v}k_{w}}{2m} \right] {s_{v}s_{w}} \\
& = \frac{1}{4m} s^\intercal Bs
\end{flalign}
$$
$B$ used here is called the modularity matrix. the 1/2 is omitted for ease of computing.

---
Categories: [[Network Science]], [[050-Statistics]]
References:
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC1482622/
https://neo4j.com/blog/graph-algorithms-neo4j-louvain-modularity/
https://en.wikipedia.org/wiki/Modularity_(networks)
Created: 2024-05-22
