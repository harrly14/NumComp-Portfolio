---
aliases:
  - SVD
---
A factorization that exists for every matrix, written

$$A = U\Sigma V^T$$

where $U$ and $V$ have [[Orthogonality#Orthonormal vectors and orthogonal matrices|orthonormal columns]] and $\Sigma$ is diagonal with non-negative entries. The entries of $\Sigma$ are called the singular values, and they are ordered from $\sigma_{\max}$ down to $\sigma_{\min}$.

Thinking of orthogonal matrices as rotations and reflections, the SVD says any matrix can be written as: rotate/reflect ($V^T$), scale along the coordinate axes ($\Sigma$), then rotate/reflect again ($U$).

# Low-rank approximation
Because the singular values are ordered from largest to smallest, you can keep only the first $k$ of them and the matching columns of $U$ and $V$ to get a rank-$k$ matrix. This truncation is the best rank-$k$ approximation of $A$. 

The idea is that each singular value says how much $A$ stretches along one direction, so dropping the small ones discards the least important directions, similar to how [[Newton's method]] approximates a root by truncating the taylor series.

# Role in Numerical Computation
The SVD gives a third way to solve a [[Least squares|least squares]] problem. Compute $U^Tb$, solve with the diagonal $\Sigma$, then apply $V$ for a total cost of $2mn + 2n^2$ per right-hand side.

