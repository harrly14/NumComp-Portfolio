A matrix whose columns are a basis of functions evaluated at a set of discrete points

# The formula

$$
V(x) = \begin{bmatrix}
1 & x_{1} & x_{1}^2 & \dots \\
1 & x_{2} & x_{2}^2 & \dots \\
\vdots & \vdots & \vdots & \ddots
\end{bmatrix}
$$

# Role in Numerical Computation
With a Vandermonde, we can reframe a polynomial as a matrix $V$.

If you want to evaluate a polynomial, you would find values $y$ given coefficients $p$ such that $Vp = y$. On the other hand, if you wanted to fit a polynomial to data, you would find coefficients $p$ given values $y$ such that $Vp = y$.

When $V$ is square there are as many basis functions as data points, so the fit passes exactly through every point, which is [[Polynomial interpolation]]. With more points than basis functions, it becomes a [[Least squares|least squares]] problem.

The columns do not have to be powers of $x$. Any set of basis functions gives a matrix of the same shape, such as the [[Chebyshev polynomials|Chebyshev basis]]. All of these span the same polynomials, but the matrices have different [[Conditioning#Conditioning of matrices|condition numbers]]. The monomial Vandermonde matrix on equally spaced points is very ill-conditioned, and its condition number grows quickly with the number of points. Changing the basis, the placement of the points, or both can improve it.