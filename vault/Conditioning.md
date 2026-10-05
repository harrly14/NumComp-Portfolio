---
aliases:
  - conditioned
  - ill-conditioned
  - well-conditioned
---
Conditioning is an inherent property of the mathematical problem itself. It is independent of any algorithm or code you write. 

Well-conditioned: Small changes in the input $x$ produce small changes in the output $f(x)$.

Ill-conditioned: Small changes in the input cause massive, wildly disproportionate swings in output

If a problem is ill-conditioned, no algorithm can fix it. You cannot code your way around a bad mathematical foundation. 

# Measuring conditioning
Absolute condition number ($\hat{\kappa}$): if $f(x)$ is differentiable, this is simply the derivative. Otherwise, we use the limit definition of the derivative at that point

Relative condition number ($\kappa$): Because [[Floating-Point Arithmetic]] relies on relative accuracy, this is the more useful metric. It scales the absolute condition number by the inputs and outputs $$\kappa = |f'(x)| \left| \frac{x}{f(x)} \right|$$
A problem becomes highly ill-conditioned (large $\kappa$) under any of these circumstances:
- the derivative is huge
- the input $x$ is huge
- the output $f(x)$ is tiny (most common)

# Conditioning of matrices
The definition above also makes sense when inputs and outputs are vectors -- just replace each absolute value with a [[Norm|norm]]. Consider matrix-vector multiplication, $f(x) = Ax$:

$$\kappa = \max_{\delta x} \frac{\|A\delta x\|}{\|\delta x\|}\,\frac{\|x\|}{\|Ax\|} = \|A\|\,\frac{\|x\|}{\|Ax\|}$$

where $\|A\|$ is the [[Norm#Induced matrix norm|induced matrix norm]]. This depends on $x$. Example: $A = \begin{bmatrix} 1 & 0 \\ 0 & 0 \end{bmatrix}$ has $\kappa = 1$ at $x = [1,0]^T$, but at $x = [0,1]^T$ we get $Ax = 0$, so $\kappa$ is infinite.

The condition number of the matrix is the worst case over all vectors:
$$\kappa(A) = \max_{x \neq 0} \|A\|\,\frac{\|x\|}{\|Ax\|}$$

If $A$ is invertible, write $x$-dependence in terms of $y = Ax$ and this simplifies to

$$\kappa(A) = \|A\|\,\|A^{-1}\|$$

So multiplying by a matrix is exactly as ill-conditioned as solving a linear system with that matrix.

## Condition number via SVD
In terms of the [[Singular value decomposition]] $A = U\Sigma V^T$, the condition number is the ratio of the extreme singular values:

$$\kappa(A) = \frac{\sigma_{\max}}{\sigma_{\min}}$$

Orthogonal transformations don't change the singular values, so they don't change the conditioning either.

# Conditioning and Rootfinding
The conditioning of rootfinding depends on the problem's input representation, rather than just the function itself. A polynomial can be specified by its coefficients or by its roots, as can be seen easily in [[Wilkinson's polynomial]]. These two representations act as different inputs to the same problem, and the map from coefficients to roots can be much more ill-conditioned than the reverse. In particular, roots that are close to each other tend to make the rootfinding problem ill-conditioned. See the image in [[Wilkinson's polynomial]] for an example. 