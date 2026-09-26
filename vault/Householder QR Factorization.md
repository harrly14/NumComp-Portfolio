An alternative way to compute a [[QR Factorization]] by directly triangularizing $A$ with a sequence of [[Orthogonality|orthogonal]] [[Reflectors|reflections]], rather than orthogonalizing its columns.

# The idea
[[Gram-Schmidt Orthogonalization]] builds $Q$ by projecting each column onto what came before it. [[Projector|Projections]] are rank-deficient operations, and applying a chain of them is what makes Gram-Schmidt numerically fragile. Householder inverts the approach. Instead of building $Q$ out of $A$, it looks for a sequence of orthogonal reflectors that reduce $A$ down to $R$.

Gram-Schmidt solves $A = QR$. Householder instead solves $Q^TA = R$, and only assembles $Q$ afterward if it's needed.

# The algorithm
Each step uses one reflector to zero out everything below the diagonal in a single column, without changing the columns already finished. The steps are: 
1. Take the entries of the current column, from the diagonal down.
2. Build a reflector that collapses that piece of the column onto a single axis so everything below the diagonal becomes zero, while the vector's length is preserved.
3. Apply that reflector to the remaining unfinished part of the matrix.
4. Move to the next column and repeat on the smaller submatrix that's left.

After working through every column, what remains is $R$. $Q$, if needed, is just the product of every reflector applied along the way.

$$
\underbrace{\begin{bmatrix} * & * & * \\ * & * & * \\ * & * & * \\ * & * & * \\ * & * & * \end{bmatrix}}_{A}
\to
\underbrace{\begin{bmatrix} * & * & * \\ 0 & * & * \\ 0 & * & * \\ 0 & * & * \\ 0 & * & * \end{bmatrix}}_{Q_1 A}
\to
\underbrace{\begin{bmatrix} * & * & * \\ 0 & * & * \\ 0 & 0 & * \\ 0 & 0 & * \\ 0 & 0 & * \end{bmatrix}}_{Q_2 Q_1 A}
\to
\underbrace{\begin{bmatrix} * & * & * \\ 0 & * & * \\ 0 & 0 & * \\ 0 & 0 & 0 \\ 0 & 0 & 0 \end{bmatrix}}_{Q_3 Q_2 Q_1 A}
$$

# Role in Numerical Computation
Householder QR is [[Stability|backward stable]] because aech step is an orthogonal transformation. As such, it is the fix for the instability seen in [[Gram-Schmidt Orthogonalization|Gram-Schmidt]], at the cost of no longer building $Q$ as you go.