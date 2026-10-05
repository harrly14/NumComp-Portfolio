The length of a vector, induced by the [[Inner product]]. Norm is denoted with double bars $\|$. A vector with $\|x\| = 1$ is called a unit vector. Normalization is the process of turning a vector into a unit vector by dividing it by its own length.

# The formula

$$\|x\| = \sqrt{x^Tx}$$

This is a generalization of the Pythagorean theorem

# Matrix norm
A matrix norm is induced by a choice of vector norm. It measures the most that $A$ can stretch a vector.

$$\|A\| = \max_{x \neq 0} \frac{\|Ax\|}{\|x\|}$$

Because $A$ is linear, only the direction of $x$ matters, so this can equivalently be written $\|A\| = \max_{\|x\| = 1} \|Ax\|$.

The matrix norm is what defines the [[Conditioning|condition number of a matrix]].

# Role in Numerical Computation
Normalization shows up in [[Gram-Schmidt Orthogonalization]], which normalizes each new [[Orthogonality|orthogonal]] vector to build an [[Orthogonality#Orthonormal vectors and orthogonal matrices|orthonormal basis]], and the projection formula simplifies a great deal when the vector you're projecting onto is already a unit vector.