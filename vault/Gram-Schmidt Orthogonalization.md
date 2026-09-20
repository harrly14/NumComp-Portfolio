---
aliases:
  - Gram-Schmidt
---

An algorithm that takes any set of vectors and produces an [[Orthogonality|orthogonal]], or more accurately [[Orthogonality|orthonormal]], basis for their span.

# The algorithm
For each vector, in order:
1. Take the next vector.
2. Project it onto everything already orthogonalized so far, and sum those projections.
3. Subtract that total projection off the vector.
4. Normalize what's left. This is the next orthonormal basis vector.

# Role in Numerical Computation
Applying this to the columns of a matrix $A$ one at a time is exactly how you build the [[QR Factorization]]. 

Note: the order in which projections are subtracted (one at a time vs. all at once from the original vector) has a big effect on numerical accuracy. Computing all projections against the original vector up front loses orthogonality much faster than updating the vector after each subtraction.