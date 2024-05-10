---
tags:
  - Statistics
---
Say we have a vector $X \in R^n$ where $X_i$ are the traits of $X$.
$$
X = 
\begin{pmatrix}
X_{1} \\
X_{2} \\
\vdots \\
X_{n}
\end{pmatrix} \\
$$
and for each trait $X_{p}$, we can define its mean $\mu_p$. Suppose there's an underlying common factor $f \in R^p$ which can explain the derivation of each trait $X_i$ from its mean and some specific factor $\epsilon_i$, and we can say trait $X_i$ is explained by this latent factor and noise $\epsilon$:
$$
\begin{flalign}
X_{i} & = \mu_{i} + l_{i1}f_{1} + l_{i2}f_{2} + \dots + l_{ip}f_{p} + \epsilon_{i} \\
& = \mu_{i} + l_{i}^Tf + \epsilon_{i}
\end{flalign}
$$
Here, the coefficients $l_{ij}$ are called factor loadings.
Then,
$$
\begin{align} \\
X_{1} & = \mu_{1} + l_{11}f_{1} + l_{12}f_{2} + \dots + l_{1p}f_{p} + \epsilon_{i} \\
X_{2} & = \mu_{2} + l_{22}f_{2} + l_{22}f_{2} + \dots + l_{2p}f_{p} + \epsilon_{i} \\
X_{3} & = \mu_{3} + l_{33}f_{3} + l_{32}f_{2} + \dots + l_{3p}f_{p} + \epsilon_{i} \\
\dots \\
X_{n} & = \mu_{n} + l_{nn}f_{n} + l_{n2}f_{2} + \dots + l_{np}f_{p} + \epsilon_{i} \\
\end{align}
$$
Therefore,
$$
X = 
\begin{pmatrix}
\mu_{1} \\
\mu_{2} \\
\mu_{3} \\
\dots \\
\mu{n}
\end{pmatrix} + 
\begin{pmatrix}
l_{11}  & l_{12} & l_{13} & \dots l_{1p} \\
l_{21}  & l_{22} & l_{23} & \dots l_{2p} \\
l_{31}  & l_{32} & l_{33} & \dots l_{3p} \\
\dots \\
l_{n1}  & l_{n2} & l_{n3} & \dots l_{np} \\
\end{pmatrix} \\
f +
\begin{pmatrix}
\epsilon_{1} \\
\epsilon_{2} \\
\epsilon_{3} \\
\dots \\
\epsilon_{n}
\end{pmatrix}
$$
$$
\therefore X = M + Lf + E
$$


## References
https://online.stat.psu.edu/stat505/book/export/html/691

Created: 2024-05-03