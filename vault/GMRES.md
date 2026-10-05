Generalized Minimum Residual. An iterative method for solving $Ax = b$ that, at iteration $n$, picks the vector in the [[Krylov subspace]] that minimizes the residual:

$$\min_x |Ax - b| \quad \text{over } x \in \text{span}(Q_n)$$

It only needs to apply $A$, never to see its entries.

# Derivation
Using the basis $Q_n$ from [[Arnoldi iteration]], write $x = Q_ny$ for some $y$. The Arnoldi relation $AQ_n = Q_{n+1}H_n$ turns the problem into

$$|Q_{n+1}H_ny - b|$$

Since $Q_{n+1}$ has orthonormal columns and $b$ lies in its span, this is equivalent to

$$|H_ny - Q_{n+1}^Tb|$$

and because $q_1 = b / \|b \|$, we have $Q_{n+1}^Tb = \|b \|e_1$, so the problem becomes

$$\Big| H_ny - \|b \|e_1 \Big|$$

This is a small $(n+1) \times n$ least squares problem. It is solved by incrementally updating a [[QR Factorization]] of $H_n$ as each new column arrives.