---
aliases:
  - Newton form
  - Newton basis
  - Newton interpolation
---
Newton polynomials are a polynomial basis built from products of $(x - x_i)$ over the data points, chosen so that the interpolation matrix becomes triangular.

# The idea
Given distinct points $x_0, \dots, x_m$, the Newton basis polynomials are

$$n_k(x) = \prod_{i=0}^{k-1}(x - x_i)$$

so $n_0 = 1$, $n_1 = (x - x_0)$, $n_2 = (x - x_0)(x - x_1)$, and so on. The [[Vandermonde matrix]] system for [[Polynomial interpolation|interpolation]] becomes

$$\big[\, 1 \mid (x - x_0) \mid (x - x_0)(x - x_1) \mid \cdots \,\big]\, p = y$$

The columns are just one choice of basis. The polynomial you get is the same as with any other basis, but the matrix is different.

# Why the matrix is triangular
Evaluate the basis at a data point $x_j$. Every $n_k$ with $k > j$ contains the factor $(x - x_j)$, so it equals $0$ there. The entry in row $j$, column $k$ is therefore $0$ whenever $k > j$, which means everything above the diagonal is zero. This is a lower triangular matrix.

# Role in Numerical Computation
Newton polynomials show that a different choice of basis can change the structure of the problem. The monomial Vandermonde matrix is dense, and the Lagrange basis makes it the identity. The Newton basis sits in between, with a matrix that is triangular, so it needs a cheap solve but not zero work.