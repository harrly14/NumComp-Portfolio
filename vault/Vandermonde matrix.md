A matrix whose columns are a basis of functions evaluated at a set of discrete points

# The  formula

$$V(x) = \begin{bmatrix}
1 & x_{1} & x^2_{2} & \dots \\
1 & x_{2} & x^2_{2} & \dots \\
\vdots & \vdots & \vdots & \ddots
\end{bmatrix}$$

# Role in Numerical Computation
With a Vandermonde, we can re-frame a polynomial as a matrix $V$. 

If you want to evaluate a polynomial, you would find values $y$ given coefficients $p$ such that $Vp = y$. On the other hand, if you wanted to fit a polynomial to data, you would find coefficients $p$  given values $y$ such that $Vp = y$. 