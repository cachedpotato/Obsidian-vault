---
tags:
---
# Kullback-Leibler Divergence
The Kullback-Leibler divergence measures how different two distributions (often times model $Q$ and real distribution $P$) are from each other, and is defined as:
$$
D_{KL}(P||Q) = \sum_{x \in \mathcal{X}}P(x)\log\left( \frac{{P(x)}}{Q(x)} \right)
$$

## Relationship with entropy
A quick reminder that the entropy of a distribution is defined as:
$$
H_{P}(X) := -\sum_{x\in\mathcal{X}}P(x)\log(P(x))
$$
Therefore, the KL-divergence can be rewritten as
$$
\begin{align}
D_{KL}(P||Q) &= \sum_{x \in \mathcal{X}}P(x)\log\left( \frac{{P(x)}}{Q(x)} \right) \\
&= \sum_{x \in \mathcal{X}}(P(x)\log(P(x)) - P(x)\log(Q(x))) \\
&= H(P,Q) - H(P)
\end{align}
$$

Therefore, we can view the KL-divergence as the element of _excess "surprise"_ we get by using model distribution $Q$ rather than the real distribution $P$. In other words, it measures the _relative increase in entropy_ by changing distributions, hence why this metric is also known as **relative entropy**.

Also rearranging the above equation gives the relationship between KL-divergence and cross entropy:
$$
H(P, Q) = H(P) + D_{KL}(P||Q)
$$
Therefore, cross entropy can be viewed as a sum of 1) the original entropy of distribution $P$ and 2) the relative entropy of $P$ with respect to $Q$.

## Asymmetry
We can easily misjudge this as a distance metric, however this cannot be further from the truth. Distance requires that it is symmetrical, that is to say,
$$
d(P, Q) = d(Q, P)
$$
Let's see if cross entropy has this property. $$ \begin{align} D_{KL}(P||Q) &= \sum_{x \in \mathcal{X}}P(x)\log\left( \frac{{P(x)}}{Q(x)} \right) \\ D_{KL}(Q||P) &= \sum_{x \in \mathcal{X}}Q(x)\log\left( \frac{{Q(x)}}{P(x)} \right) \\
\therefore D_{KL}(P||Q) &\neq D_{KL}(Q||P)
\end{align}
$$
Furthermore, KL-divergence can go to the negatives. Technically speaking, KL-divergence is not a "metric". Efforts to make it into a metric lead to what's called the Jensen-Shannon divergence.

## Jensen-Shannon divergence
Also known as the information radius (IRad) or total divergence to the average, the Jensen-Shannon divergence is a **metric** that measures the similarity of two [[Probability Distribution]]. It is defined by:

$$
JSD(P||Q) = \frac{1}{2}D(P||M) + \frac{1}{2}D(Q||M) \quad where \quad M=\frac{1}{2}(P+Q)
$$
The distribution $M$ is a mixture distribution of $P$ and $Q$, defined in the KL-divergence section above. a more general definition (multiple distributions) would be:

$$
\begin{align} \\
JSD_{\pi_{1}, \pi_{2},\dots,\pi_{n} }(P_{1},P_{2},\dots,P_{n}) &= \sum_{i}\pi_{i}D(P_{i}||M) \\
&= H(M) - \sum_{i}\pi_{i}H(P_{i})
\end{align}
$$
where
$$
\begin{align}
M&:=\sum_{i}\pi_{i}P_{i} \\
\sum_{i}\pi_{i} &= 1
\end{align}
$$
and $\pi_{i}$ is the weight of distribution $P_i$.

Given two distributions $P$ and $Q$, the Jensen-Shannon Divergence is bounded by 1 given that we use a base 2 logarithm. For a more general bound, assuming we are using base $b$ logarithm, the divergence is bound by:
$$
0\leq JSD_{\pi_{1}, \pi_{2},\dots,\pi_{n} }(P_{1},P_{2},\dots,P_{n}) \leq \log_{b}(n)
$$

---
Categories: [[050-Statistics]], [[Information Theory]]
References:
