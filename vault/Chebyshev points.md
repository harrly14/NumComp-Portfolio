---
aliases:
---
Cosine-spaced points are a way of placing [[Polynomial interpolation|interpolation]] points on an interval so that they bunch up near the ends instead of being evenly spread.

# The idea
On $[-1, 1]$, take equally spaced angles $\theta_k$ from $-\pi$ to $0$ and use their cosines as the points:

$$x_k = \cos\theta_k$$

On a general interval $[a, b]$, scale and shift the result:

$$x_k = \frac{a+b}{2} + \frac{b-a}{2}\cos\theta_k$$

# How it relates to Chebyshev polynomials
This is the same angle variable used to define the [[Chebyshev polynomials]], where $x = \cos\theta$. The points are equally spaced in $\theta$ rather than in $x$.

The points and the basis are separate choices. Cosine-spaced points can be paired with the monomial basis, and the Chebyshev basis can be paired with equally spaced points.

# Role in Numerical Computation
Where the points go matters as much as which basis is used. Cosine-spaced points with the Chebyshev basis give an error that keeps shrinking. The same points also keep the condition number of the interpolation matrix from growing, but only as long as the basis is good too.