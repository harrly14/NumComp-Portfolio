Given an $m \times n$ matrix $A$ with $m \ge n$, find $x$ that minimizes

$$|Ax - b|$$

If $A$ is square and full rank, the minimizer satisfies $Ax - b = 0$. In general that isn't possible, because $b$ is not in the range of $A$. Instead, the residual $Ax - b$ must be [[Orthogonality|orthogonal]] to the range of $A$.

# Why [[QR Factorization|QR]] works
$QQ^T$ is an orthogonal [[Projector|projector]] onto the range of $Q$. If $A = QR$,

$$QQ^T(Ax - b) = QQ^T(QRx - b) = Q(Q^TQ)Rx - QQ^Tb = QRx - QQ^Tb = Ax - QQ^Tb$$

So if $b$ is in the range of $A$, we can just solve $Ax = b$. If not, we only need to orthogonally project $b$ onto the range of $A$ first.

# Ways to solve it
1: QR ([[Householder QR Factorization|Householder]])
Solve $Rx = Q^Tb$. This is stable and accurate. 

2: Normal equations ([[Cholesky QR Factorization|Cholesky]])
Uses the mathematically equivalent system $(A^TA)x = A^Tb$. It involves factoring the symmetric  matrix $A^TA = R^TR$. The catch is that forming $A^TA$ squares the [[Conditioning|condition number]], which can reduce the accuracy of the least squares solution.

3: [[Singular value decomposition|SVD]]
With $A = U\Sigma V^T$, compute $U^Tb$, solve with the diagonal $\Sigma$, and apply $V$. 

| Method                      | Total cost                                                                     | Where and why to use it                                                                                                                                                                        |
| --------------------------- | ------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| QR (Householder)            | $2mn^2 - \tfrac{2}{3}n^3$ to factor once, then $4mn - n^2$ per right-hand side | The default. It is stable and accurate, and the factorization is reused across right-hand sides.                                                                                               |
| Normal equations (Cholesky) | $mn^2 + \tfrac{1}{3}n^3$ to factor once, then $2mn + 2n^2$ per right-hand side | When speed matters and $A$ is well-conditioned. It is the cheapest, but squaring the condition number can cost accuracy, so avoid it for ill-conditioned $A$.                                  |
| SVD                         | about $2mn^2 + 11n^3$ to factor once, then $2mn + 2n^2$ per right-hand side    | When you want the most information about $A$ (the singular values give $\kappa(A)$) or $A$ is rank deficient. It costs about the same as QR when $m \gg n$, but much more for square matrices. |
# Role in Numerical Computation
Fitting a polynomial to data with a [[Vandermonde matrix]] is a least squares problem, and QR is the stable way to solve it. [[GMRES]] also reduces to a small least squares problem at each iteration.