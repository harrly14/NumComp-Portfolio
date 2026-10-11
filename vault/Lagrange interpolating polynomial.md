---
aliases:
---
The Lagrange form writes the [[Polynomial interpolation|interpolating polynomial]] directly in terms of the data, with no linear system to solve.

# The idea
Given values $y_0, \dots, y_m$ at distinct points $x_0, \dots, x_m$, the interpolating polynomial of degree $m$ is

$$p(t) = \sum_{i=0}^m y_i \prod_{j \ne i} \frac{t - x_j}{x_i - x_j}$$

Each product is a polynomial $L_i(t)$ that equals $1$ at $x_i$ and $0$ at every other data point. The formula builds $p$ by scaling each $L_i$ by its data value $y_i$ and adding them up. The $L_i$ are called the Lagrange basis polynomials.

<iframe src="./supplements/lagrange.htm" title="Animated construction of the Lagrange interpolating polynomial" style="width:100%; aspect-ratio:16/10; min-height:440px; border:0; border-radius:8px; display:block;" loading="lazy"></iframe>

Each basis polynomial $L_i$ is $1$ at $x_i$ and $0$ at the other nodes; scaling by $y_i$ and summing recovers $p$.

# Role in Numerical Computation
The Lagrange form is the extreme case of choosing a basis to make the interpolation matrix easy -- the matrix becomes the identity, so nothing needs to be solved. The cost moves into evaluating the formula, and the form is awkward for other tasks, such as converting to standard form or taking derivatives.

It is also a useful way to study the conditioning of interpolation. Because the form is just a function of the data, the [[Conditioning#Conditioning of matrices|condition number]] depends on the input and is hard to explore directly. Instead, interpolation is studied as a linear map from data values to values of the interpolant, whose columns are the Lagrange polynomials. How sensitive the interpolant is to the data is then a question about the condition number of that map, which depends on where the points are placed. 