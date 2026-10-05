An [[Orthogonality|orthogonal]] transformation that flips a vector across a plane. Used to rearrange a vector without changing its length.

A [[Projector]] $I-vv^T$ keeps everything orthogonal to $v$. Subtracting $vv^T$ twice instead of once instead sends the part of the vector along $v$ to the other side of the plane orthogonal to $v$, flipping it instead of flattening it. 

Applying a reflector twice undoes it and returns the original vector.

![[Pasted image 20260926120519.png]]

# Building a reflector that zeroes out a vector
Given some vector $x$, choosing $v = ‖x‖e_{1} - x$ produces a reflector that sends $x$ to a multiple of $e_1$ so every entry after the first becomes zero, and the length of $x$ is preserved. This is what makes reflectors useful for triangularizing a matrix one column at a time.

If $x$ points nearly in the same direction as $e_{i}$, then the first entry of the above vector $v$ subtracts nearly equal numbers, which causes [[Stability|cancellation]]. If $x$ is exactly along $e_{i}$, $v$ becomes zero and normalizing it produces NaN. To fix this, reflect $x$ onto either $+\| x \|e_{i}$ or $-\| x \|e_{i}$ is farther from $x$. Doing so makes $v$ as long as possible, so nothing cancels.
![[Pasted image 20261004183542.png]]
# Role in Numerical Computation
Reflectors are used in [[Householder QR Factorization]]. Reflectors are chained together to triangularize a matrix without ever giving up the stability that orthogonal transformations provide.