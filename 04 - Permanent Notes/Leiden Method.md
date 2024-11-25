---
tags:
---
# Leiden Method
Leiden Method, or Leiden Clustering, is an improvement over the [[Louvain Method]]. The Louvain method, while simple and quite powerful, can lead to "badly connected" or at worst disconnected clusters. 

To ensure communities are well connected, the Leiden Method incorporates a "refinement" step on top of Louvain method. A refined partition $\mathscr{P_{\mathrm{refined}}}$ is a subcommunity of partition $\mathscr{P}$ that was determined in the "movement of nodes step" (Louvain method step 1). 
![[41598_2019_41695_Fig3_HTML.webp|500]]
Unlike in the first step where nodes are moved greedily to partitioned that will yield the most increase in modularity. Instead, the node is merged randomly to any community that increases the quality function.

Leiden Method also incorporates a faster method of local movement by using a faster, "pruning" algorithm. Instead of visiting all nodes, Leiden Method will only visit nodes whose neighborhood has changed. First, the nodes in the network are queued in a random order. As we go down the queue, if a node is moved to a different community, then the neighboring nodes of the community that are not yet in the queue is added to the rear end. 


## Guarantees
Aside from the increase in speed by virtue of the new local movement method, Leiden Method also has some guarantees that Louvain Method does not provide:
1) All communities are $\gamma$-connected: Louvain method can sometimes have disconnected communities, but Leiden method will ensure all nodes within a partition is connected.
2) All communities are subpartition $\gamma$-dense: This means that the communities, if partitioned into two parts, they are i) well connected to each other; ii) neither part can be separated from its community; and iii) each part is also subpartition $\gamma$-dense itself.
3) All communities are uniformly $\gamma$-dense: no subsets of the community can be separated from the community. 
4) All communities are subset optimal: all subsets of the community are locally optimally assigned.


## Performance
As can be seen from the image below, Leiden Method is better than Louvain Method in every way. 
![[41598_2019_41695_Fig4_HTML.webp]]

---
Categories: [[Community Detection]], [[Clustering]]
References:
https://www.nature.com/articles/s41598-019-41695-z
