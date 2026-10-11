---
aliases:
---
The Chebyshev polynomials are a family of polynomials defined through the cosine, which makes a well-conditioned [[Polynomial interpolation|interpolation]] basis when paired with good points.

# The idea
The $n$-th Chebyshev polynomial is defined by

$$T_n(x) = \cos\big(n \arccos(x)\big)$$

on $[-1, 1]$. Substituting $x = \cos\theta$ turns it into $T_n(\cos\theta) = \cos(n\theta)$, so $T_n$ is a cosine wave in the angle $\theta$, drawn as a function of $x$. Because it is a cosine, its values always stay between $-1$ and $1$ on $[-1, 1]$.

Let $y = \arccos x$. The angle-sum identity gives
$$T_{n+1}(x) = \cos(ny)\cos y - \sin(ny)\sin y, \qquad T_{n-1}(x) = \cos(ny)\cos y + \sin(ny)\sin y$$

Adding the two, the sine terms cancel and $\cos y = x$, so $T_{n+1} + T_{n-1} = 2x\,T_n$. This gives the recurrence

$$T_0 = 1, \qquad T_1 = x, \qquad T_{n+1} = 2x\,T_n - T_{n-1}$$

Each step multiplies by $x$ and subtracts, so every $T_n$ is a polynomial of degree $n$.

# As an interpolation basis
Using $\{T_0, T_1, \dots, T_{n-1}\}$ as the columns gives a [[Vandermonde matrix]] built from the recurrence instead of from powers of $x$. It spans the same polynomials as the monomials, so it produces the same interpolant but a different matrix.

# Role in Numerical Computation
The Chebyshev basis is a well-conditioned replacement for the monomial basis, an example of fixing instability by changing the basis. The [[Conditioning|condition number]] of its matrix stays small when the points are [[Chebyshev points|cosine-spaced]], but it still grows on equally spaced points.