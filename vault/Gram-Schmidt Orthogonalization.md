---
aliases:
  - Gram-Schmidt
---
An algorithm that takes any set of linearly independent vectors and produces an [[Orthogonality|orthogonal]], or more accurately [[Orthogonality|orthonormal]], basis for their span.

# The algorithm
For each vector, in order:
1. Take the next vector.
2. [[Projector|Projects]] it onto everything already orthogonalized so far, and sum those projections.
3. Subtract that total projection off the vector.
4. Normalize what's left. This is the next orthonormal basis vector.

# Classical vs. modified
There are two ways to organize the subtraction step: 
1. Classical: computes the projection of the original vector on all previous columns of Q, then subtracts them all at once
2. Modified: subtracts each projection immediately, so every later projection is computed against what's left over, not the original vector.

Mathematically, these two methods produce the same answer. In practice, we are dealing with [[Floating-Point Arithmetic]] and the Classical method can lose [[Orthogonality]] very quickly once the input vectors are close to linearly dependent. The Modified method, however, is more [[Stability|stable]] and loses orthogonality more slowly.

The distinction of when to use one method over the other isn't purely based on stability. The Classical method doesn't need to know all the vectors in advance, since each new vector is only compared to the bases already built, so it is the natural choice for applications like streaming data, where vectors arrive one at a time. The Modified method is more reliable, but only reaches its efficient form when reorganized to be right-looking (below), which requires having every vector available from the beginning.

# Left vs. right looking
Describes when each column's contribution gets computed. Left-looking looks backward at the previously finished columns and uses them to remove components from the current vector. Right-looking uses a new orthonormal column as soon as its finished to remove its component from every unifinished column to the right.

Right-looking organization does operations over many remaining columns at once, providing more parallelism and being more efficient in cases where you have all the vectors from the start.

# Role in Numerical Computation
Applying this to the columns of a matrix $A$ one at a time is exactly how you build the [[QR Factorization]]. 