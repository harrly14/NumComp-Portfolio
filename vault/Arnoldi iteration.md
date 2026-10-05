An algorithm that builds an orthonormal basis for a [[Krylov subspace]] without ever forming the ill-conditioned Krylov matrix. It applies orthogonal similarity transformations to reduce $A$ to Hessenberg form (zero below the first subdiagonal), starting from $q_1 = b / \|b \|$:

$$A = QHQ^T$$

Multiply on the right by $Q$ and look at only the first $n$ columns:

$$AQ_n = Q_{n+1}H_n$$

Here $Q_n$ is $m \times n$, $Q_{n+1}$ is $m \times (n+1)$, and $H_n$ is an $(n+1) \times n$ Hessenberg matrix. This identity is what makes [[GMRES]] work.