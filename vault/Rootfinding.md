Rootfinding is the computational process of finding a value $x$ such that a given function $f(x) = 0$. 

Rootfinding is more important that finding where a graph crosses an axis, it also is a translator for solving equations. Almost any math problem or model can be rearranged into a rootfinding problem by moving all terms to one side of the equal sign. For example, to find where two curves intersect($g(x) = f(x)$), you can rewrite it as the rootfinding problem $f(x) - g(x) = 0$. 

For linear or quadratic equations, we have exact algebraic formulas, but for complex non-linear equations like $e^x - \sin(x) = 2$ or something, no exact formula exists. We must use numerical algorithms to guess and iteratively refine the answer.

Real world examples of rootfinding could be: 

| Forward model `f`                                                                                       | Rootfinding application                                                                             |
| ------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| Position of a ball after it is thrown                                                                   | How to throw the ball to hit the target (what angle and force to throw it)                          |
| Nitrogen soil cycling: a time series of nitrogen in a plot as it stabilizes and reaches an equiplibrium | Using a target stable nitrogen level, find what initial inputs would stabilize at that target level |
| input of data                                                                                           | interpolant, or the line that goes through all the data                                             |
All rootfinding algorithms trade off between speed, computational cost, and guarentee of successs.

## Methods:
- [[Bisection Method]]
- [[Newton's method]]
- [[Fixed-Point Iteration]]