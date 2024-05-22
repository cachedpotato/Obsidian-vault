---
tags:
---
# Dimensionality Reduction
The data we deal with have high number of features, meaning it's high dimensional. Take patient's genome data for example. even if we count just "a few thousand" marker genes littered throughout their entire genome, that's 1000 dimensions. Even if we know how to mathematically cluster/classify data, we can't comprehend let alone visually how it actually lies in such high-dimensional spaces. Hence the need for dimensionality reduction was born.

Dimensionality Reduction aims to visualize high-dimensional data by projecting into a low-dimensional (often 2D) surface and at the same time visualize how the processed/preprocessed data points lie. There are multiple ways of doing this.

## Categories of Dimensionality Reduction Methods
Dimension reduction algorithms fall into 2 categories.

### Prioritizing pairwise distance structure amongst all data samples
- [[Principal Component Analysis]]
- MDS
- Sammon mapping

### Prioritizing the local structure over global structure
- [[T-distributed Stochastic Neighbor Embedding]]
- [[Uniform Manifold Approximation and Projection]]
- Isomap
- LargeVis
- Laplacian eigenmaps

---
Categories: [[Statistics]], [[Data Visualization]]
References:
https://arxiv.org/abs/1802.03426
Created: 2024-05-21
