A way to algebraically measure the angle and magnitude between two vectors. This is especially important for vectors that do not lie within $R^2$, because we otherwise would not have an easy way to visually see and measure these relationships. 

# The formula

$$x^Ty = \sum_{i} x_{i} y_{i}$$
This is the same formula as the dot product; inner product is the more general name, whereas the dot product is the specific inner product used for real-valued vectors. 

# Angle between vectors
Following from the inner product and [[Norm]], the angle between two vectors is: 

$$\cos \theta = \frac{x^Ty}{\| x \| \| y \|}$$

# Role in Numerical Computation
From the inner product, we get [[Norm]] (length of a vector), angle, and [[Orthogonality]]. It also generalizes past vectors, as two functions can be checked for orthogonality using the same formula. 