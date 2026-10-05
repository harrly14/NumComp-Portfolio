---
aliases:
  - Cholesky
---
An alternative way to compute a [[QR Factorization]] by reading R off the matrix AᵀA with a Cholesky factorization, then recovering Q from A.

# The idea
If $A = QR$, then

$$A^TA = (QR)^T QR = R^TQ^TQR = R^TR$$

since $Q^TQ = I$. A Cholesky factorization $LL^T = A^TA$ gives exactly this kind of triangular factor, so $R = L^T$. Once $R$ is known, $Q = AR^{-1}$.

Unlike [[Gram-Schmidt Orthogonalization]] and [[Householder QR Factorization]], this never orthogonalizes columns or applies reflectors. It computes $R$ first and gets $Q$ afterward.

# The algorithm

1. Form $A^TA$.
2. Compute its Cholesky factorization and take $R = L^T$.
3. Recover $Q = AR^{-1}$ by solving a triangular system.

# Where it breaks
Cholesky QR can fail because of forming $A^TA$ (which is also what makes it cheap) because it squares the [[Conditioning|condition number]]. When the columns of $A$ are nearly parallel (as with a [[Vandermonde matrix]]), every entry of $A^TA$ is nearly the same, and the small differences that actually separate the columns get lost to rounding (See [[Stability|cancellation]]). $R$ comes out slightly wrong, and $Q = AR^{-1}$ inherits that error, so $Q$ is no longer [[Orthogonality|orthogonal]]. In bad cases the Cholesky factorization itself can fail.

Still, $QR$ does reproduce $A$. The product is accurate, but $Q$ is not orthogonal.

The fix is to run Cholesky QR twice. The first pass gives $Q_{1}$ and $R_{1}$, where $Q_{1}$ is not orthogonal but is far better conditioned than $A$. The second pass applies Cholesky QR to $Q_{1}$, giving $Q$ and $R_{2}$. This works because squaring a condition number close to 1 does little damage, so the second pass is accurate and cleans up the leftover error.

The two passes combine into one factorization:

$$A = Q_1R_1 = (QR_2)R_1 = Q(R_2R_1)$$

# Role in Numerical Computation
Cholesky QR is a cheap-looking alternative, but fewer steps does not guarantee faster. On a 5000×1000 matrix, Julia's built-in `qr` took 0.17s and used about 38 MB, while the two-pass Cholesky QR took 0.20s and used about 114 MB. Profiling (`@profview`) is how you find out where the time actually goes.