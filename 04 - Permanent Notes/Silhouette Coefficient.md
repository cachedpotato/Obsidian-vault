---
tags:
---
# Silhouette Coefficient
When we want to measure how adequate our cluster numbers/formation are, one simple way to find out is by comparing the minimum distance between different clusters and distance of data points within the same cluster. One way of doing this is by utilizing the silhouette coefficient.

let $a(i)$ be the average distance between points in cluster $i$. Then,
$$
a(i) = \frac{1}{|C_{I}|-1}\sum_{j \in C_{I}, i \neq j}d(i, j)
$$
Where $|C_{I}|$ indicates the number of points in cluster $I$.

similarly, we can define the mean dissimilarity of point i to some cluster $C_{J}$ like so:
$$
b(i) = \min_{J\neq I}\frac{1}{|C_{J}|-1}\sum_{j \in C_{J}}d(i, j)
$$
In other words,$b(i)$ indicates the _minimum_ distance between point I and some other cluster $J$. Now, we can define the silhouette coefficient $s(i)$ as the following:

$$
s(i) = \frac{{b(i) - a(i)}}{\max\{a(i), b(i)\}}, \quad if |C_{I}| > 1
$$
From here, we can see that $-1\leq s(i)\leq1$. the smaller the $a(i)$, and the bigger the $b_{i}$, the closer to 1 the silhouette coefficient will be, which is the ideal output. If the clusters are not well defined, The value will be a lot lower than 1.

Clustering with average silhouette of 0.7 is considered strong, 0.5 reasonable, and 0.3 weak.


---
Categories: [[Performance Metric]], [[Clustering]]
References:
https://en.wikipedia.org/wiki/Silhouette_(clustering)
Created: 2024-05-21
