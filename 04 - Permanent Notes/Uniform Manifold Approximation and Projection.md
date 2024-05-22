---
tags:
  - NeedWork
---
# Uniform Manifold Approximation and Projection
Uniform Manifold Approximation and Projection (UMAP) is a dimensionality reduction method based on Riemannian geometry and algebraic topology.

## The Math
...is what I would write down if I knew category theory. what the hell even is Riemannian geometry? I'll come back to this later. Probably.

## High Level Explanation
UMAP is another case of k-neighbor graph based algorithms. First said k-neighbor weighted graph is created, then a low-dimensional version of this is computed, under the following assumptions/axioms:

- There exists a [[Manifold|manifold]] on which the data would be uniformly distributed.
- The underlying manifold of interest is locally connected.
- Preserving the topological structure of this manifold is the primary goal.

Because we assume the data is uniformly distributed, given a ball of fixed size $B$ centered on some point $X_{i}$, the amount of data within the ball would be roughly the same regardless of the choice of center point. This means we can find the [[Geodesic Distance|geodesic distance]] from $X_{i}$ to its neighbors by normalizing the distances with respect to the distance to the $k^{th}$ nearest neighbors. 

This requires that we make a custom distance for each $X_{i}$, which we wish to merge into a consistent global structure (the cluster map). This is done by more magic math jargon that I'm not gonna go into right now.

## Computational View of UMAP
UMAP creation can be divided into 2 steps: graph construction and graph layout.
### Graph Construction
Given dataset $X = \{x_1, ... , x_n\}$, and metric (dissimilarity measure) $d: X \times X \to R_{\geq0}$ , we compute the k-nearest neighbors set $\{x_{i_{1}}, x_{i_{2}}, ... x_{i_{k}}\}$. Let
$$
\rho_{i} = \min\{d(x_{i}, x_{i_{j}})| 1 \leq j \leq k, \quad d(x_{i}, x_{j}) >0\}
$$
be the nearest neighbor of the k-neighbors and let $\sigma_i$ be such a value that
$$
\sum_{j=1}^k\exp\left( -\frac{\max(0, d(x_{i}, x_{i_{j}}) - \rho_{i})}{\sigma_{i}} \right) = \log_{2}k
$$
the $\sigma$ here acts as a normalization factor.
Now, we can define our graph $\overline G = (V, E, \omega)$. the $w$ here is the weight of the edges, given by:
$$
w((x_{i}, x_{i_{j}})) = \exp\left( -\frac{\max(0, d(x_{i}, x_{i_{j}}) - \rho_{i})}{\sigma_{i}} \right)
$$

Let $A$ be the weighted adjacency matrix of $\overline G$, which can be interpreted as the probability matrix of an edge existed between given vertices. Let
$$
B = A^\intercal + A + A\circ A^\intercal
$$
which can be interpreted as the probability of an edge existing between two vertices in an undirected graph. The UMAP graph $G$ takes such $B$ as the weighted adjacency matrix.

### Graph Layout
Now that we defined our UMAP graph $G$, it's time to make a graph layout algorithm.

- attractive force between vertices $y_i, \quad y_j$
$$
\frac{-2ab||y_{i}-y_{j}||_{2}^{2(b-1)}}{1 + ||y_{i} - y_{j}||^2_{2}}w((x_{i}, x_{j}))(y_{i}, y_{j})
$$
- Repulsive force between vertices $y_i, \quad y_j$
$$
\frac{2b}{(\epsilon + ||y_{i}-y_{j}||^2_{2})(1 + a||y_{i}-y_{j}||^2_{2})} (1 - w((x_{i}, x_{j})))(y_{i} - y_{j})
$$
---
Categories: [[Dimensionality Reduction]]
References:
https://arxiv.org/abs/1802.03426
Created: 2024-05-21
