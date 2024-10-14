---
tags:
---
# MA Plot
MA plot is a type of visual representation of genomic data, visualizing the differences taken in two samples. The plot transforms data into M (log ratio) and A (mean average) scales.
$$
\begin{align} \\
M &= \log_{2}(S_{1}/S_{2}) = \log_{2}S_{1} - \log_{2}S_{2}\\
A &= \frac{1}{2}\log_{2}(S_{1}S_{2}) = \frac{1}{2}(\log_{2}S_{1} + \log_{2}S_{2})
\end{align}
$$
$S_{1}$ and $S_2$ are the measurements from the two samples, which are often times the intensity measurement from microarray assays. The x axis is interpreted as the number of hits, and the y axis is interpreted as the degree of differential expression of a given gene (data point).

Here's an example of an MA plot:
![[Xu_2018a.png|400]]
The leftmost datapoints are often ignored because of their low average hit rate (not enough to draw statistical conclusions). the further up/down the y axis, the more up-regulated/down-regulated the genes are. the cutoff for the log ratio will differ by the type of dataset being used, but is normally between 1.5~2.

---
Categories: [[050-Statistics]], [[Bioinformatics]]
References:
