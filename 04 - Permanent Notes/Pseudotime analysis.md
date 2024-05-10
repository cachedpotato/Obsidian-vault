---
tags:
  - Bioinformatics
---
### Overview
Pseudotime analysis is used to get a view, or rather, the change of expression by "time", using a collection of high-dimensional molecular data from a cross-sectional cohort. 

![[스크린샷 2024-05-03 102743.png |550]]

We first put the patient data into a one-dimensional space (pseudotime), and from here we can do various analysis with pseudotime as the axis. for example, we can measure gene expression change over time, or even PCA, with colors as pseudotime.


### The Math
Pseudotime Analysis is based on [[Factor Analysis]].
Let $Y$ be a $N \times G$ matrix. $y_{ng}$ then, is the expression info of gene $g$ of sample $n$. $y_{ng}$ then, is a linear combination of some latent measure $z_n$ and a factor loading for g:
$$
y_{ng} = \lambda_{g}z_{n} + \epsilon_{ng}, \epsilon_{ng} \sim N(0, \tau_{g}^{-1})
$$
This would be the case if it weren't for covariates that also affect the output y but cannot be explained by $z_n$ alone. Let such covariates $X$ be an $N \times P$ matrix where $P$ is normally smaller than $N$. We allow such $X$ to perturb our factor loading matrix:
$$
\lambda_{g} \to \lambda_{ng} = \lambda_{g} + \sum_{p=1}^p \beta_{pg}x_{np}
$$
Where $\beta$ quantifies the effect to which covariate perturbs our factor loading matrix.
In summary, $y$ can be explained by, or in other words, a linear combination of, 1) covariate $x$ and 2) latent measure $z$ which is also determined by 3) factor loading $g$ :
$$
\begin{flalign}
y_{ng} & = \eta_{g} + \sum_{p = 1}^p \alpha_{pg}x_{np} + \left( \lambda_{g} + \sum_{p=1}^p \beta_{pg}x_{np} \right)z_{n} \\
& = \eta_{g} + x_{n}^T\alpha_{g} + (\lambda_{g} + x_{n}^T\beta_{g})z_{n}
\end{flalign}
$$
marginalizing over $g$ gives:
$$
y_{n} = Ax_{n}^T + \lambda z_{n} + Bx_{n}^Tz_{n} + \epsilon_{n}
$$

![[스크린샷 2024-05-03 141717.png |500]]

## References
https://www.nature.com/articles/s41467-018-04696-6

Created: 2024-04-30