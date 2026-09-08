---
aliases:
  - bisection
---
A [[Rootfinding|rootfinding]] technique that uses the Intermediate Value Theorem and does not require derivative information

# The algorithm
Start with an interval `[a,b]` where the function crosses the x-axis somewhere in the interval. Calculate the midpoint $\frac{a+b}{2} = c$ and check the sign of $f(c)$. Replace $a$ or $b$ depending on which on shares the same sign as $f(c)$ with the new point $c$. Repeat until the interval is smaller than a tolerance.

# Strengths
If a continuous function changes sign within the interval, bisection is guaranteed to converge on a root. Unlike [[Newton's method]], you always know exactly what your maximum error is at any given stage, because it is simply half the width of the current bracket.

# Weaknesses
Bisection is somewhat slow, as it has a linear rate of [[Convergence|convergence]]. It gains roughly one bit of accuracy per iteration. You also have to know roughly where the root is beforehand to supply the initial interval, which can be a problem. Also, it does not work when the function touches the x-axis but does not cross it (like $f(x) = x^{2}$ for example), because there is no sign change.