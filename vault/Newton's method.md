---
aliases:
  - Newton-Raphson Method
  - Newton's
linked_lectures: 2026-09-04
---
Newton's method, also known as Newton-Raphson method, is a [[Rootfinding|rootfinding]] algorithm which progressively finds better and better approximations for the roots of a function. While significantly faster than the [[Bisection Method]], it requires a good initial guess and information about the derivative of the function.

# The algorithm
The formula is derived by truncating the [[Taylor Series]] expansion of the function. We approximate the function as a line starting from our original guess $x_{k}$:

$$f(x) \approx f(x_{k})+f'(x_{k})(x-x_{k}) = 0$$

Solving for $x$ gives us our next guess, $x_{k+1}$:

$$x_{k+1} = x_k - \frac{f(x_k)}{f'(x_k)}$$


In simple terms, the algorithm works by using an initial guess `x0`, then drawing a tangent line to the function `f` at point `x0`. This tangent line is necessarily the derivative `fp(x0)`. Then, follow that tangent line to the x-axis and repeat, using the point where the line intercepts the x-axis as your new guess.

# Convergence
Newton's Method is a specific type of [[Fixed-Point Iteration]] where the iteration function is that of the tangent line formed at $x_k$:

$$g(x) = x - \frac{f(x)}{f'(x)}$$

To know if this loop closes is on the root rather than spiraling out of control, we can use [[Mean value Theorem]] (MVT) and [[Taylor Series]]. MVT shows that the error will shrink as long as the slope of $g(x)$ near the root is shallow (less than 1). The Taylor Series shows that the error $e_{k+1} \approx g'(x^*) \cdot e_{k}$ where $x^*$ is the actual root of the function. For most algorithms, this proves the error drops by a steady percentage each loop ([[Convergence|q-linear convergence]]) 

However, more can be shown than just q-linear convergence. In Newton's Method, 
$$g'(x^*)= \frac{f(x)f''(x)}{[f'(x)]^2}$$
At the root, $f(x^*) = 0$, so $g'(x) = 0$. From the Taylor Series, we had: 

$$e_{k+1} = g'(x^*)e_{k} + \frac{1}{2}g''(x^*)e^{2}_{k}+\dots$$

We can see that because the first derivative of $g$ at $x^*$ is $0$, the entire first term dissapears. The remaining terms are dominated by the $e^2_{k}$ term as $h$ gets small (recall the distinction to numerical computation's [[Big-O]] notation). Thus, Newton's Method is locally **q-quadratic convergence**.


# Vulnerabilities
How well this algorithm converges relies heavily on the first guess we use and the function's shape. It can fail if:
-  $f'(x^*)$ is close to 0 (flat spots), the tangent line intercepts the x-axis very far away from $x_{0}$, causing our next guess to be very different. This is further reinforced by the math above, because in out calculation of $g'(x^*)$, if $f'(x^*)$ is close to $0$, the whole equation blows up and breaks. This rootfinding  problem is [[Conditioning|ill-conditioned]] near shallow curves, making the algorithm [[Stability|unstable]].
- Certain initial guesses for some functions can cause the algorithm to bounce back and forth between two points indefinitely without every converging
- If the function is a parabola resting on the x-axis, that means the root is where both $f(x) = 0$ and $f'(x) = 0$. In these cases, the derivative in the denominator approaches 0 along with the numerator, slowing the algorithm.
- When a root has another root very close to it, Newton's convergence degrades from quadratic to linear, and the iteration can stall before getting to [[Machine Epsilon]] precision. This is because the underlying rootfinding problem is [[Conditioning|ill-conditioned]] as roots cluster. 