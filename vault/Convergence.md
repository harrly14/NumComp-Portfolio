A convergent [[Rootfinding|rootfinding]] algorithm produces a sequence of approximations $x_{k}$ that approach the true root $x^*$. For analysis, we define error at step $k$ as $e_{k}=x_{k} - x^*$.

# q-linear convergence
An iterative algorithm is q-linearly convergent if the ratio of successive errors approaches a constant factor less than 1. That is: 
$$\lim_{ k \to \infty } \frac{|e_{k+1}|}{|e_{k}|} = \rho < 1$$
Here, error drops by a steady fraction. The smaller the convergence factor ($\rho$), the faster the convergence.

# r-linear convergence
A slightly weaker condition than q-linear convergence. An algorithm has r-linear convergence if its error is simply bounded by some other sequence that is q-linearly convergent. The error itself could bounce around a bit, but its trapped beneath the ceiling of a q-linearly convergent algorithm that is dropping by a steady percentage.