Factoring a matrix $A$ into an [[Orthogonality|orthogonal]] matrix $Q$ and an upper triangular matrix $R$. 

# The idea

$$A = QR$$

$Q$ is an orthogonal matrix. $R$ is an upper triangular matrix and records how much of each new column overlapped with the orthogonalized columns before it.

# Reduced vs. Full
For $A$ of size $m\times n$ with $m > n$:
- Full QR: $Q$ is square and truly orthogonal, $R$ is $m \times n$ with zero rows below the triangle.
- Reduced QR: $\hat{Q}$ has orthonormal columns, but is not square, $\hat{R}$ is $n \times n$ upper triangular. 

The extra $m − n$ columns of the full $Q$ span the orthogonal complement of $range(A)$, and they only ever multiply the zero rows of $R$, so they contribute nothing to the product. Reduced QR drops them.

# Algorithms
- [[Gram-Schmidt Orthogonalization|Gram-Schmidt]] (naturally reduced)
- [[Householder QR Factorization|Householder]] (naturally full)
- [[Cholesky QR Factorization|Cholesky]]

# Role in Numerical Computation
Solving $Ax = b$ by substituting $A = QR$ gives $Rx = Q^Tb$ without ever having to invert a matrix, which is much cheaper. Applied to a [[Vandermonde matrix]], this is a numerically [[Stability|stable]] way to fit a polynomial to data, replacing the fragile approach of inverting $V$ directly.

When $A$ has more rows than columns (more data points than unknowns), $Ax = b$ usually has no exact solution, so we minimize $\| Ax -b \|$ instead. The columns of $Q$ span the same space as $A$, and $QQ^T$ is the [[Projector]] onto that space. The closest point to $b$ in that space is $\hat{Q}\hat{Q}^Tb$, so we need $\hat{Q}\hat{R}x = \hat{Q}^Tb$ which reduces to $\hat{R}x = \hat{Q}^Tb$. This is solved by back substitution, using reduced $\hat{Q}$. Fitting a polynomial to data with a [[Vandermonde matrix]] is exactly this problem.