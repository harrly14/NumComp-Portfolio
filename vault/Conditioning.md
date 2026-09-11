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

Relative condition number ($\kappa$): Because [[Floating-Point Arithmetic]] relies on relative accuracy, this is the more useful metric. It scale the absolute condition number by the inputs and outputs $$\kappa = |f'(x)| \left| \frac{x}{f(x)} \right|$$
A problem becomes highly ill-conditioned (large $\kappa$) under any of these circumstances:
- the derivative is huge
- the input $x$ is huge
- the output $f(x)$ is tiny (most common)

# Conditioning and [[Rootfinding]]
The conditioning of rootfinding depends on the problem's input representation, rather than just the function itself. A polynomial can be specified by its coefficients or by its roots, as can be seen easily in [[Wilkinson's polynomial]]. These two representations act as different inputs to the same problem, and the map from coefficients to roots can be much more ill-conditioned than the reverse. In particular, roots that are close to each other tend to make the rootfinding problem ill-conditioned. See the image in [[Wilkinson's polynomial]] for an example. 