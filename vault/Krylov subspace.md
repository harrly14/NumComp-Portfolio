The Krylov subspace is the space spanned by a vector $b$ and its repeated products with a matrix $A$:

$$K_n(A, b) = \text{span}(b, Ab, A^2b, \dots, A^{n-1}b)$$

As a matrix, the basis vectors are the columns of

$$K_n =[ b \mid Ab \mid A^2b \mid \dots \mid A^{n-1}b]$$

This is the natural place to look for an approximate solution to $Ax = b$ when you can only apply $A$ and can't see its entries. Each new basis vector costs one multiplication by $A$.

However, $K_n$ is horribly [[Conditioning|ill-conditioned]]. This means $K_n$ can't be computed stably as written. The fix is to never form it, and to build an [[Orthogonality#Orthonormal vectors and orthogonal matrices|orthonormal]] basis $Q_n$ for the same space instead. As a factorization, this would be

$$K_n = Q_nR_n$$

where the first column $q_1 = b / \| b \|$, but the $R_n$ is unnecessary and hopelessly ill-conditioned, so it is skipped. [[Arnoldi iteration]] builds $Q_n$ directly, without ever forming $K_n$ or $R_n$.

Krylov subspaces are the foundation of [[GMRES]].