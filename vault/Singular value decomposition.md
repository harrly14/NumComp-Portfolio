---
aliases:
  - SVD
---

A factorization that exists for every matrix, written

$$A = U\Sigma V^T$$

where $U$ and $V$ have [[Orthogonality#Orthonormal vectors and orthogonal matrices|orthonormal columns]] and $\Sigma$ is diagonal with non-negative entries. The entries of $\Sigma$ are called the singular values, and they are ordered from $\sigma_{\max}$ down to $\sigma_{\min}$.

Thinking of orthogonal matrices as rotations and reflections, the SVD says any matrix can be written as: rotate/reflect ($V^T$), scale along the coordinate axes ($\Sigma$), then rotate/reflect again ($U$).

# Role in Numerical Computation
The SVD gives a third way to solve a [[Least squares|least squares]] problem. Compute $U^Tb$, solve with the diagonal $\Sigma$, then apply $V$ for a total cost of $2mn + 2n^2$ per right-hand side.
