---
aliases:
  - interpolation
---
Interpolation is finding a function that passes exactly through a given set of data points. Polynomial interpolation does this with a single polynomial, and the interesting question is not whether one exists but how reliably you can compute it. Interpolation is different than extrapolation which attempts to make estimations outside the range of current data. 

# The idea
Given data $(x_i, y_i)$ for $i = 1, \dots, n$ where each $x_i$ is distinct, find $f$ such that $f(x_i) = y_i$ exactly. Unlike [[Least squares]], there is no closest fit. Instead, the curve is forced through every point. With polynomials, there is exactly one polynomial of degree at most $n-1$ that does this. 
# As a linear system
Each point gives one equation, so the equations stack into a [[Vandermonde matrix]] system:

$$V p = y$$

Here $V$ has one row per data point and one column per basis function. Interpolation is the square case, with as many basis functions as data points ($m = n$). 

Using $\{1, x, x^2, \dots\}$ is only one choice of basis. Any basis for polynomials of degree below $n$ works. A different basis gives a different matrix $V$ and different coefficients $p$, but the same polynomial.

# Two different conditioning questions
There are two relevant condition numbers, and they measure different things.
1. The [[Conditioning#Conditioning of matrices|condition number]] of the matrix $V$ tells you how much error is amplified when solving for the coefficients $p$. This depends on both the basis and the points.
2. The interpolation operator is the map from data values $y$ to the values of the interpolant at a set of evaluation points $s$. In matrix form it is $V(s)V(x)^{-1}$, where $V(s)$ is the same basis evaluated at the points $s$. Because the interpolant is unique, the basis cancels and this depends only on the points. Its condition number is the ratio of extreme singular values [[Conditioning#Condition number via SVD|via the SVD]], and the singular vector for the largest one is the data pattern that gets amplified most.

The first is a property of the algorithm (a way of computing the polynomial). The second is a property of the problem, similar to the split of [[Conditioning]] versus [[Stability]]. A bad basis makes $V$ ill-conditioned, but you can change basis and fix it. A bad choice of points, on the other hand, makes the operator itself ill-conditioned, and no basis can fix it.

# Basis and points
Comparing common choices of basis and spacing of points, all on $[-1, 1]$. We investigate how the condition number of $V$ behaves as the number of points $n$ grows:

| Basis                                                                 | Equally spaced points                                   | Cosine-spaced points                       |
| --------------------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------ |
| Monomial $\{1, x, x^2, x^3, \dots\}$                                  | Worst: grows the fastest                                | Still grows, but more slowly               |
| Legendre $\{1, x, \tfrac{3x^2 - 1}{2}, \tfrac{5x^3 - 3x}{2}, \dots\}$ | Starts slowly, then picks up                            | Stays roughly flat                         |
| Chebyshev $\{1, x, 2x^2 - 1, 4x^3 - 3x, \dots\}$                      | Still grows, but more slowly than monomial              | Best: small rise at first, then levels off |

Only both a good basis and good points together keep the matrix well-conditioned. Fixing just one (monomial on cosine-spaced points or Chebyshev on equally spaced points) slows the growth but doesn't stop it.

The operator's condition number does not depend on the basis at all. That is the part a better basis cannot remove, and it is controlled only by where the points are.

# Role in Numerical Computation
Polynomial interpolation is the cleanest case study for separating the problem from the algorithm. The polynomial is the same whichever basis you use, so any difference in accuracy comes from how you compute it. The practical recipe is two separate choices: pick points that keep the operator well-conditioned, then pick a basis that keeps the matrix well-conditioned. Fitting a polynomial with the monomial [[Vandermonde matrix]] on equally spaced points fails on both counts at once.