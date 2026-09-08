---
aliases:
---
Fixed-point iteration is an open [[Rootfinding|rootfinding]] technique that turns a standard equation $f(x) = 0$ into the form $x = g(x)$. A "fixed point" is a value that remains exactly the same after the function $g$ is applied to it. If you can find the fixed point of $g(x)$, you have simultaneously found the root of $f(x)$. 

# The algorithm
Rearrange you original equation $f(x) = 0$ to isolate $x$ on one side, defining your new function $g(x)$. Note that there are algebraically infinite ways to do this, but choosing the right one dictates if your algorithm succeeds or not. Take an initial guess $x_{0}$ to get your next guess via $x_{k+1} = g(x_{k})$. Repeat until $x_{k+1}$ and $x_{k}$ are identical, or until you reach a stopping criteria.

# [[Convergence]] & [[Stability]]
The [[Mean value Theorem]] (MVT) proves whether or not the algorithm works by connecting the new error to the old error using the function's slope: 
$$e_{k+1} = g'(c) \cdot e_{k}$$
For the error to shrink, the slope multiplier must be between -1 and 1. Therefore, a fixed-point iteration only converges if $|g'(x)| < 1$ near the true root.

A [[Taylor Series]] expansion shows how fast the algorithm works by mapping the error algebraically: 
$$e_{k+1} \approx g'(x^*)\cdot e^k + \frac{g''(x^*)}{2}e^2_{k}$$
Because the dominant term is $e_{k}$ (recall the numerical computation definition of [[Big-O]]) and it is to the first power, the algorithm has linear [[Convergence|convergence]]. The error shrinks by a steady percentage $g'(x)^*$ on every loop.

# Connections
[[Newton's method]] is an optimized specific version of Fixed-Point iteration where the algebraic rearrangement is $g(x) = x - \frac{f(x)}{f'(x)}$. It is powerful because $g'(x^*)$ is exactly 0, resulting in quadratic convergence by wiping out the linear error term.