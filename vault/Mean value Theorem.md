---
aliases:
  - MVT
---
A calculus theorem guaranteeing that, for any smooth continuous curve between two points, there is at least one point in the middle where the instantaneous slope (or tangent line) perfectly matches the average slope between the endpoints. 

# The formula
If $f(x)$ is continuous on $[a,b]$ and differentiable on $(a.b)$, there exists some point $c$ in the interval such that 
$$f'(c) = \frac{f(b) - f(a)}{b-a}$$
# Role in Numerical Computation
In numerical analysis, the MVT is used as an error-bounding tool. By rearranging the formula into $f(b) - f(a) = f'(c)(b-a)$, we can show how distances like the gap between a guess and a true root scale from one step to the next based on the function's derivative. 