---
aliases:
  - orthogonal
---

The higher-dimensional generalization of perpendicular. Two vectors are orthogonal when their [[Inner product]] is zero.

# The formula

$$x^Ty = 0$$

This follows from requiring that , $\| x - y \| = \| x - (-y) \|$, which is the distance-based definition of a right angle. Expanding both sides algebraically collapses to $x \cdot y = 0$.

# Orthonormal vectors and orthogonal matrices
Two vectors are orthonormal if they're orthogonal to each other and both [[Norm|unit vectors]]. A matrix whose columns are all orthonormal is an orthogonal matrix (conventionally called $Q$, $U$, or $V$).

# Role in Numerical Computation

Orthogonal vectors carry independent information, so projecting one onto the other gives nothing. This is the property that projections are built to test for (the leftover piece of a projection is always orthogonal to what you projected onto), and it's the property [[Gram-Schmidt Orthogonalization]] tries to manufacture across an entire set of vectors.

Orthogonal matrices are powerful because their inverses are just their transposes, and transposes cost pretty much nothing to compute, as compared to inverses. So, any time you can arrange for a matrix in a computation to be orthogonal, you can invert it for free. This is the motivation behind [[QR Factorization]]