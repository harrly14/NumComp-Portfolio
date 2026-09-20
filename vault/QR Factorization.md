Factoring a matrix $A$ into an [[Orthogonality|orthogonal]] matrix $Q$ and an upper triangular matrix $R$, produced by running [[Gram-Schmidt Orthogonalization|Gram-Schmidt]] on $A$'s columns.

# The formula

$$A = QR$$

$Q$ is an orthogonal matrix. $R$ is an upper triangular matrix and records how much of each new column overlapped with the orthogonalized columns before it.

# Role in Numerical Computation
Solving $Ax = b$ by substituting $A = QR$ gives $Rx = Q^Tb$ without ever having to invert a matrix, which is much cheaper. Applied to a [[Vandermonde matrix]], this is a numerically [[Stability|stable]] way to fit a polynomial to data, replacing the fragile approach of inverting $V$ directly.