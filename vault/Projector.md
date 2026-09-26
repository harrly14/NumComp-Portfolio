---
aliases:
---
An operation that flattens a vector onto a subspace. Can be thought of as the shadow of a vector on another vector
![[Pasted image 20260926114110.png]]

For a unit vector $v$, $vv^T$ is a projector. Applying $vv^T$ to any vector $x$ keeps only the part of $x$ pointing along $v$ and discards the rest. The complementary matrix $I - vv^T$ is a projector that does the opposite. That is, it keeps everything [[Orthogonality|orthogonal]] to $v$ and discards the part along $v$. Together, the two split any vector into two pieces that add back up to the original.

# Why it's rank-deficient
Once a projector is applied once, applying it more times does nothing. That also means that a projector can't be undone, because whatever landed in its nullspace cannot be recovered from the output. This is what separates a projector from a [[Reflectors|reflector]], which rearranges a vector without discarding information.

# Role in Numerical Computation
[[Gram-Schmidt Orthogonalization]] sequentially removes each vector's projection (applying $I-vv^T$ one direction at a time) onto the directions already found, normalizing what's left over to build an orthogonal matrix $Q$.